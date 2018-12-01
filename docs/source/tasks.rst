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
    dotnet run --no-build -- --config goerli
    
4. Launch Nethermind with spaceneth testnet config. Spaceneth is your private, local network that will have no blocks at the beginning.

::
 
    cd src/Nethermind/Nethermind.Runner
    dotnet run --no-build -- --config spaceneth
    
5. Visit `ethstats <https://ethstats.net/>`_ and analyze the network parameters and nodes. Ask questions about the meaning of anything that is not clear.

6. Download `beige paper <https://github.com/chronaeon/beigepaper/blob/master/beigepaper.pdf>`_ and analyze available EVM opcodes in Appendix A.

7. Launch Nethermind spaceneth again and leave it open in a separate window - leave it running for the time of the workshop. Next run a tool that we are going to use to analyze the EVM behaviour (it accepts bytecode and returns Geth-like trace of the transaction)

::

    cd src/Nethermind/Nethermind.Runner
    dotnet run --no-build -- --config spaceneth
    
::

    cd src/Nethermind/Nethermind.EvmPlayground
    dotnet run --no-build
    
