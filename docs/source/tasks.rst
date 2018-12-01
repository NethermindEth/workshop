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
    
8. Write a simple code in EvmPlayground that will execute '2 + 2'

::

     0x60 2 0x60 2 0x01 0x00
     
9. Now write different bytecodes that will:
 * cause StackUnderflowException
 * cause BadInstructionException

10. Analyze opcodes JUMP, JUMPI, JUMPDEST and write bytecode that will:
 * cause StackOverflowException

11. Analyze MSTORE, MLOAD operations and write bytecode that will:
 * store 32 bytes in memory at position 0
 * store 32 bytes in memory at position 1
 * store 32 bytes in memory at position 32
 * store 0x2a in memory at position 31
 * store 0x2a in memory at position 0

12. Analyze RETURN opcodes and write bytecode that will:
 * return 42

13. Analyze opcodes SSTORE, SLOAD and write bytecode that will:
 * permanently store information that address 0x00010203040506070809000a0b0c0d0e0f00010203 has 1 Ether
 
14. Each EvmPlayground call is in fact sending an Init type transaction to spaceneth which in turn deploys a contract with bytecode equal to the EvmPlayground call return value (like the one in '12)'). Write bytecode that will
 * deploy code from '8)' 
 
15. Analyze CALL, CALLCODE (deprecated), DELEGATECALL, STATICCALL and write bytecodes that will
 * call the contract deployed in '14)' (you will need to check address where the contract was deployed)
 * cause StaticCallViolationException
 
16. Analyze CALLDATALOAD opcode and write code that will
 * improve the code deployed in '14)' to alow the calculator to add any two 256-bit numbers
 
17. Check what do the opcodes between 0x30 and 0x3e do and experiment with them in EvmPlayground

17. Check what do the opcodes between 0x40 and 0x45 do and experiment with them in EvmPlayground
 * write bytecode that will run a loop that will use the entire block gas limit if the block number is even and will do nothing if the block is odd
