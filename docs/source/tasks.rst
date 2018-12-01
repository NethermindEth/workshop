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

3. Launch Nethermind with goerli testnet config and wait until it synchronizes fully. You can check the latest block on Goerli testnet in `Goerli explorer <https://blockscout.com/eth/goerli/>`_ or at `Goerli ethstats <https://stats.goerli.net/>`_. After Nethermind synchronizes entire Goerli network press 'e' to close Nethermind.

::
 
    cd src/Nethermind/Nethermind.Runner
    dotnet run -- --config goerli

4. Launch Nethermind with goerli testnet config

::
 
    cd src/Nethermind/Nethermind.Runner
    dotnet run -- --config goerli
    
5. Launch Nethermind with spaceneth testnet config. Spaceneth is your private, local network that will have no blocks at the beginning.

::
 
    cd src/Nethermind/Nethermind.Runner
    dotnet run -- --config spaceneth
    
6. Visit `ethstats <https://ethstats.net/>`_ and analyze the network parameters and nodes. Ask questions about the meaning of anything that is not clear.

7. Download `beige paper <https://github.com/chronaeon/beigepaper/blob/master/beigepaper.pdf>`_ and analyze available EVM opcodes in Appendix A.
