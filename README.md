# Python 3.10 : What's the new ?

The release of ✨Python 3.10✨ is getting closer, so it's time to take a ride with the new version of Python and see what awesome new features will come with this new release👌 😍. 

## Install Python 3.10 Alpha version

To try these new features, we will have to install the Alpha/Beta version of Python 3.10. Remember that this last version is not yet stable. 
- If you are under Linux (Ubuntu), you just have to follow the steps below : 

     ```sh
     # Download the latest version for Linux
     wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0a6.tgz
     # Unpack Python source code
     tar xzvf Python-3.10.0a6.tgz
    cd Python-3.10.0a6
    # Compile Python source with static libraries
    ./configure --prefix=$HOME/python-3.10.0a6
    make
    make install
    $HOME/python-3.10.0a6/bin/python3.10
    ```
- If you are under Windows, you just have to **Download Python Executable** Installer from [here](https://www.python.org/ftp/python/3.10.0/python-3.10.0a6-amd64.exe), then you need to **Run Executable Installer**. 
- If you are on MacOs, I can't help you. I am not rich enough to buy a Mac!!! 😒, but this [link](https://opensource.com/article/19/5/python-3-default-mac) may help you. 

Yeeeep, Python 3.10 is finally installed ✌ , now we can take a look at all the new features . Let's start 😉😎. 

### New Type Union Operator
Instead of using typing.union to express the syntax **"either type X or type Y"**, the new version of python introduces the new union operator of type *X | Y*. This new operator allows us to code more cleanly and efficiently.




