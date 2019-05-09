Build
*****

IDE
++++++++++++++++

* JetBrains Rider https://www.jetbrains.com/rider/
* VS Code https://code.visualstudio.com/docs/other/dotnet

SDKs
++++

You will need .NET SDK 2.2
 * Windows https://www.microsoft.com/net/download?initial-os=windows
 * Linux https://www.microsoft.com/net/download?initial-os=linux (make sure to select the right distribution)
 * Mac https://www.microsoft.com/net/download?initial-os=macos

Linux
+++++

::

    sudo apt-get update && sudo apt-get install libsnappy-dev libc6-dev libc6

MacOS
+++++

::

    brew install gmp
    brew install snappy

Note: MacOS users may encounter an error when starting the node claiming that "rocksdb is not found". A quick fix for this is running the command below (IMPORTANT: This is a quick fix that **should not be used** other than for testing and education purposes.

::

    brew install rocksdb
    
This will install the latest version of rocksdb externally from Nethermind.
    
Windows
+++++++

you may need to install https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads

Docker
+++++++

**Disclaimer: Only follow the docker steps if you have used docker before or proceed at your own risk. There will be limited support for the docker flow in the workshops so you will be expected to get this working on your own.**

First Clone the repository as shown in the `All Platforms` Section:

::

    git clone https://github.com/nethermindeth/nethermind nethworkshop --recursive -b workshop

Next go into the directory and Build the docker image (the build step may take a while as it will download an image and build the nethermind from source):

::

    cd nethworkshop
    docker build  -t nethermind  --file Dockerfile_workshop .

Finally, you can run a docker container from the image above using the following command:

::

    docker run -d -t --name spaceneth nethermind

Now you can attach a shell to this container using this command:

::

    docker exec -it spaceneth /bin/bash 

Now you may proceed to the "All Platforms" section below. Note that every time you start a new terminal window you need to attach to the container shell using the command above. So you can proceed to the section below but skip the first paragraph as this has already been performed here.

All Platforms
+++++++++++++

::

    git clone https://github.com/nethermindeth/nethermind nethworkshop --recursive -b workshop
    cd nethworkshop/src/Nethermind
    dotnet build Nethermind.sln -c Release
    
Then launch two terminals and from the nethworkshop/src/Nethermind directory:

::

    cd Nethermind.Runner
    dotnet run --no-build -c Release -- --config spaceneth

    
::

    cd Nethermind.EvmPlayground
    dotnet run --no-build -c Release
 
 
Then in the EvmPlayground window write 96 01 96 02 01 00 and press ENTER (make sure that the runner is running fine)

The screen should return a transaction receipt and the last trace entry should say:
 
::
 
     {
      "Pc": 5,
      "op": "STOP",
      "Gas": 6668622,
      "GasCost": 0,
      "Depth": 1,
      "Stack": [
        "0000000000000000000000000000000000000000000000000000000000000003"
      ],
      "Memory": [],
      "Storage": {},
      "SortedStorage": {}
    }

After this works you are ready for the workshop.

You can also launch and sync Goerli testnet (after closing previous screens):

::

    cd Nethermind.Runner
    dotnet run --no-build -c Release -- --config goerli
    
You can confirm the latest block of the Goerli tetsnet here:
https://blockscout.com/eth/goerli/

Potential Issues
++++++++++++++++

.NET Core versions
^^^^^^^^^^^^^^^^^^

If you have some previous pre-release versions of .NET Core installed they may cause conflicts. Your case might be quite unique so best to search for help online.

RocksDB loading
^^^^^^^^^^^^^^^

If application crashes saying that rocksdb-sharp / rocksdb is failing then most likely your processor is not supporting AVX instructions. Go to the EthereumRunner.cs file and replace:

::

_dbProvider = HiveEnabled ? (IDbProvider) new MemDbProvider() : new RocksDbProvider(_initConfig.BaseDbPath, dbConfig, _logManager, _initConfig.StoreTraces, _initConfig.StoreReceipts);
                
                
with

::

_dbProvider = new MemDbProvider();

Debug / Release
^^^^^^^^^^^^^^^

It may happen that something goes wrong and you end up with a message like:
The application to execute does not exist: '/nethermind/src/Nethermind/Nethermind.Runner/bin/Debug/netcoreapp2.2/Nethermind.Runner.dll'

It is worth to note that .NET Core has two types of outputs - Debug and Release. Release builds are prepared with the -c Release switch. Make sure that you both build and run with -c Release.
