# Ultimate-debugging
Debugging guide for ULTIMATE


# Debug ULTIMATE
### 1 Install ULTIMATE 
First, install ULTIMATE with the single file ```ultimate-installer-v2.txt``` https://drive.google.com/file/d/1PM9UHvz6VIDI9Ga8syl9bNhpt77fy_Ro/view?usp=drive_link

### 2 Setup Eclipse IDE
- In Eclipse, open a workspace with the downloaded ULTIMATE folder as root.
- In File, import existing MAVEN project from "ULTIMATE_MODEL_MANAGER" folder.
- Right click in Project Explorer folder ```ultimate_model_manager``` > Run As > Maven Install. Then Maven Build. Then do Maven Test.
- Right click ```/src/main/java/headless/Headless.java``` > Run as > Run Configuration. In the left panel, find Java Application. Select your class (Headless) or create a new configuration by double-clicking Java Application. Then add in the Environment tab

  for IOs:
  
        DYLD_LIBRARY_PATH = libs/runtime
  
  Linux:
  
        LD_LIBRARY_PATH = libs/runtime

Also add the environmental variable  ```ULTIMATE_DIR=<path to ultimate/ULTIMATE_MODEL_MANAGER>```

- In Run configurations > JRE tab, select JAVASE-21
- Press Apply and close

- Open a terminal window, then do ```nano ~/.bashrc```, add at the end ```export LD_LIBRARY_PATH="/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH"``` (this is to avoid Storm not finding libstorm-cli-utilities.so.1.11.1).
- 


### 3 Setup ULTIMATE problem
 - Got o Debug > Debug configuration > Arguments tab. Type in ```Program arguments``` the input arguments required to run ULTIMATE headless (See https://github.com/ULTIMATE-YORK/ULTIMATE/tree/main-build-7). For example:
```
-pf /home/XXX/Desktop/ULTIMATE/case_studies/dummy/dummy.ultimate -m model2 -o /home/XXX/Desktop/ULTIMATE/ULTIMATE_MODEL_MANAGER/ULTIMATE_Numerical_Solver/output-dummy
```

<img width="1094" height="176" alt="image" src="https://github.com/user-attachments/assets/8aafe482-9605-4903-aad1-309385d2883f" />

### Done!


## Optional Code Changes
This contains changes to the code that are useful to help debugging, as currently, they are bugs.

#### 1) In Project.java

Line 290: Do not stop if ULTIMATE_DIR== null.

Change to:
```
if (ULTIMATE_DIR == null || ULTIMATE_DIR.equals("")) {
			errorMessages.add(String.format("ULTIMATE_DIR environment variable not set. Make sure it points to ultimate/ULTIMATE_MODEL_MANAGER"));
			configured = false;
			System.err.println("ULTIMATE_DIR environment variable not set. Make sure it points to ultimate/ULTIMATE_MODEL_MANAGER");
			Thread.dumpStack();
			System.exit(1);

		}
```

