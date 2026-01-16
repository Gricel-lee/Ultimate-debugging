# Ultimate-debugging
Debugging guide for ULTIMATE


# Debug ULTIMATE
### 1 Install ULTIMATE 
First, install ULTIMATE with the single file ultimate-installer-v2.txt
### 2 Setup Eclipse IDE
- In Eclipse, open a workspace with the downloaded ULTIMATE folder as root.
- In File, import existing MAVEN project from "ULTIMATE_MODEL_MANAGER" folder.
- Right click in Project Explorer folder ```ultimate_model_manager``` > Run As > Maven Install. Then Maven Build. Then do Maven Test.
- Right click ```/src/main/java/headless/Headless.java``` > Run as > Java. This will create a new run configuration for "Headless". Then do Run As > Run Configuration > Add in the Environment tab

  for IOs:
  
        DYLD_LIBRARY_PATH = libs/runtime
  
  Linux:
  
        LD_LIBRARY_PATH = libs/runtime

- In Run configurations > JRE tab, select JAVASE-21
- Press Apply and close
