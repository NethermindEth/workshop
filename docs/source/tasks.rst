Tasks
*****

Preparation
^^^^^^^^^^^

1. Clone Nethermind repository

::
 
    git clone https://github.com/NethermindEth/nethermind.git --recursive


2. Build Nethermind project following the instructions from `Nethermind readme <https://github.com/NethermindEth/nethermind/blob/master/README.md>`_.

::
 
    cd src/Nethermind
    dotnet build -c Release

3. Launch Nethermind with goerli testnet config

::
 
    cd src/Nethermind/Nethermind.Runner
    dotnet run -- --config goerli
