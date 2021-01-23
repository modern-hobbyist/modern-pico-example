# Example Pico Project with CLION
Hello! This is an example project I configured to develop and build Raspberry Pi Pico projects on my Mac in JetBrains 
CLION IDE.

There were some tricky steps that I needed to follow to get this working on a Mac, as well as within CLION, but I'm 
documenting them here for my own reference as well as for others!

# Assumptions
* You are on a Mac (though this process would be ***similar*** on Windows and Linux)
* You have some experience with command line or you are willing to learn

# Prerequisites
* CLION is installed 
* You have a terminal of some sorts (can be done within CLION's built in terminal)

# Setup for Mac
* Install Brew
    ```commandline
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
* Install the Toolchain
    ```commandline
    brew install cmake
    brew tap ArmMbed/homebrew-formulae
    brew install arm-none-eabi-gcc
    ```
* Point Your Project to the SDK
    * More information on this topic can be found at the [Pico Repository](https://github.com/raspberrypi/pico-sdk)
        * If you follow option 1 in their instructions, you will need to add the SDK path to CLION
            * Open `Preferences->Build, Execution, & Depoloyment->CMake`
            * For `Environment`, add the following
                ```commandline
                    DPICO_SDK_PATH=/path/to/your/pico-sdk/
                ``` 
    * For my purposes, I cloned the SDK as a submodule in my project.
        * Clone the SDK as a submodule called
            ```commandline
                git submodule add https://github.com/raspberrypi/pico-sdk.git
            ```
        * Setup a CMakeLists.txt like:
            ```commandline
                cmake_minimum_required(VERSION 3.12)
    
                # initialize pico_sdk from submodule
                # note: this must happen before project()
                include(pico-sdk/pico_sdk_init.cmake)
                
                project(my_project)
                
                # initialize the Pico SDK
                pico_sdk_init()
                
                # rest of your project
            ```
          
# Build!