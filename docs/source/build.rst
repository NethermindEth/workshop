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
    dotnet run -c Release
    
::

    cd Nethermind.EvmPlayground
    dotnet run -c Release
