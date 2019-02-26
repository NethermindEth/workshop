Build
*****

IDE
^^^

* JetBrains Rider https://www.jetbrains.com/rider/
* VS Code https://code.visualstudio.com/docs/other/dotnet

SDKs
^^^^

You will need .NET SDK 2.2
* Windows https://www.microsoft.com/net/download?initial-os=windows
* Linux https://www.microsoft.com/net/download?initial-os=linux (make sure to select the right distribution)
* Mac https://www.microsoft.com/net/download?initial-os=macos

Linux
^^^^^

::

    sudo apt-get update && sudo apt-get install libsnappy-dev libc6-dev libc6

MacOS
^^^^^

::

    brew install gmp
    brew install snappy
    
Windows
^^^^^^^

you may need to install https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads

All Platforms
^^^^^^^^^^^^^

::

    git clone https://github.com/tkstanczak/nethermind nethworkshop --recursive -b workshop
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
