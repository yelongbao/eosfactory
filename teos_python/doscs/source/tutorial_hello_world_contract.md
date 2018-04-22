# Tutorial Hello World Contract

We will now create our first "hello world" contract. Create a new folder called "hello" somewhere, where read-write rights are not limited:
```
import os
import pprint
import teos

contract_dir = "/mnt/e/Workspaces/EOS/logos/contracts/hello/"
if not os.path.exists(contract_dir):
    os.makedirs(contract_dir)
```
Create an empty file "hello.cpp":
```
hello_cpp = open(contract_dir + "hello.cpp", "w")

```
Open the `hello.cpp` file in a text editor. We recommend the *Visual Studio Code*. If you are working with the [*Windows Subsystem for Linux*](#https://docs.microsoft.com/en-us/windows/wsl/install-win10), the location file has to be known in terms of the *Windows* file system. It is something like `C:\Users\<username>\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState \rootfs\tmp\hello\hello.cpp`.

Copy there the following text:
```
#include <eosiolib/eosio.hpp>
#include <eosiolib/print.hpp>
using namespace eosio;

class hello : public eosio::contract {
  public:
      using contract::contract;

      /// @abi action 
      void hi( account_name user ) {
         print( "Hello, ", name{user} );
      }
};

EOSIO_ABI( hello, (hi) )
```

<!-- ```
file = open(contract_dir + "hello.cpp", "r")
print(file.read())
``` -->
You can compile your code to web assembly (.wast) as follows:
```
wast = teos.BuildCotract(contract_dir + "hello.cpp")
#  WAST file is ready.

pprint.pprint(wast.wast)
```


```
('(module\n'
 ' (type $FUNCSIG$vij (func (param i32 i64)))\n'
 ' (type $FUNCSIG$vjj (func (param i64 i64)))\n'
 ' (type $FUNCSIG$vi (func (param i32)))\n'
 ' (type $FUNCSIG$i (func (result i32)))\n'
 ' (type $FUNCSIG$iii (func (param i32 i32) (result i32)))\n'
 ' (type $FUNCSIG$vii (func (param i32 i32)))\n'
 ' (type $FUNCSIG$iiii (func (param i32 i32 i32) (result i32)))\n'
 ' (type $FUNCSIG$vj (func (param i64)))\n'
 ' (type $FUNCSIG$v (func))\n'
 ' (import "env" "action_data_size" (func $action_data_size (result i32)))\n'
 ' (import "env" "eosio_assert" (func $eosio_assert (param i32 i32)))\n'
 ' (import "env" "eosio_exit" (func $eosio_exit (param i32)))\n'
 ' (import "env" "memcpy" (func $memcpy (param i32 i32 i32) (result i32)))\n'
 ' (import "env" "printn" (func $printn (param i64)))\n'
 ' (import "env" "prints" (func $prints (param i32)))\n'
 ' (import "env" "read_action_data" (func $read_action_data (param i32 i32) '
 '(result i32)))\n'
 ' (import "env" "require_auth2" (func $require_auth2 (param i64 i64)))\n'
 ' (table 2 2 anyfunc)\n'
 ' (elem (i32.const 0) $__wasm_nullptr $_ZN5hello2hiEy)\n'
 ' (memory $0 1)\n'
 ' (data (i32.const 4) "`a\\00\\00")\n'
 ' (data (i32.const 16) "read\\00")\n'
 ' (data (i32.const 32) "Hello, \\00")\n'
 ' (data (i32.const 8448) "malloc_from_freed was designed to only be called '
 'after _heap was completely allocated\\00")\n'
 ' (export "memory" (memory $0))\n'
 ' (export "_ZeqRK11checksum256S1_" (func $_ZeqRK11checksum256S1_))\n'
 ' (export "_ZN5eosio12require_authERKNS_16permission_levelE" (func '
 '$_ZN5eosio12require_authERKNS_16permission_levelE))\n'
 ' (export "apply" (func $apply))\n'
 ' (export "memcmp" (func $memcmp))\n'
 ' (export "malloc" (func $malloc))\n'
 ' (export "free" (func $free))\n'
 ' (func $_ZeqRK11checksum256S1_ (param $0 i32) (param $1 i32) (result i32)\n'
 '  (i32.eqz\n'
 '   (call $memcmp\n'
 '    (get_local $0)\n'
 '    (get_local $1)\n'
 '    (i32.const 32)\n'
 '   )\n'
 '  )\n'
 ' )\n'
....................
```


```

abi = teos.GenerateAbi(contract_dir + "hello.cpp")
#  ABI file is ready.

pprint.pprint(abi.abi)

{'____comment': 'This file was generated by eosio-abigen. DO NOT EDIT - '
                '2018-04-22T17:11:31',
 'actions': [{'name': 'hi', 'ricardian_contract': '', 'type': 'hi'}],
 'clauses': '',
 'structs': [{'base': '',
              'fields': [{'name': 'user', 'type': 'account_name'}],
              'name': 'hi'}],
 'tables': '',
 'types': ''}
```

## Hello World Ricardian Contract

Every smart contract must have a matching [Ricardian contract](#https://en.wikipedia.org/wiki/Ricardian_contract). The Ricardian Contract specifies the legally binding behavior associated with each action of the smart contract.  

The Ricardian Contract for the Hello World Contract is listed here. It is intervened with test code, if applicable. 

### CONTRACT FOR HELLO WORLD

#### Parameters
Input paramters: NONE

Implied parameters: 

* _**account_name**_ (name of the party invoking and signing the contract)

#### Intent
INTENT. The intention of the author and the invoker of this contract is to print output. It shall have no other effect.
```

```

#### Term
TERM. This Contract expires at the conclusion of code execution.

#### Warranty
WARRANTY. {{ account_name }} shall uphold its Obligations under this Contract in a timely and workmanlike manner, using knowledge and recommendations for performing the services which meet generally acceptable standards set forth by EOS.IO Blockchain Block Producers.
  
#### Default
DEFAULT. The occurrence of any of the following shall constitute a material default under this Contract: 

#### Remedies
REMEDIES. In addition to any and all other rights a party may have available according to law, if a party defaults by failing to substantially perform any provision, term or condition of this Contract, the other party may terminate the Contract by providing written notice to the defaulting party. This notice shall describe with sufficient detail the nature of the default. The party receiving such notice shall promptly be removed from being a Block Producer and this Contract shall be automatically terminated. 
  
#### Force Majeure
FORCE MAJEURE. If performance of this Contract or any obligation under this Contract is prevented, restricted, or interfered with by causes beyond either party's reasonable control ("Force Majeure"), and if the party unable to carry out its obligations gives the other party prompt written notice of such event, then the obligations of the party invoking this provision shall be suspended to the extent necessary by such event. The term Force Majeure shall include, without limitation, acts of God, fire, explosion, vandalism, storm or other similar occurrence, orders or acts of military or civil authority, or by national emergencies, insurrections, riots, or wars, or strikes, lock-outs, work stoppages, or supplier failures. The excused party shall use reasonable efforts under the circumstances to avoid or remove such causes of non-performance and shall proceed to perform with reasonable dispatch whenever such causes are removed or ceased. An act or omission shall be deemed within the reasonable control of a party if committed, omitted, or caused by such party, or its employees, officers, agents, or affiliates. 
  
#### Dispute Resolution
DISPUTE RESOLUTION. Any controversies or disputes arising out of or relating to this Contract will be resolved by binding arbitration under the default rules set forth by the EOS.IO Blockchain. The arbitrator's award will be final, and judgment may be entered upon it by any court having proper jurisdiction. 
  
#### Entire Agreement
ENTIRE AGREEMENT. This Contract contains the entire agreement of the parties, and there are no other promises or conditions in any other agreement whether oral or written concerning the subject matter of this Contract. This Contract supersedes any prior written or oral agreements between the parties. 

#### Severability
SEVERABILITY. If any provision of this Contract will be held to be invalid or unenforceable for any reason, the remaining provisions will continue to be valid and enforceable. If a court finds that any provision of this Contract is invalid or unenforceable, but that by limiting such provision it would become valid and enforceable, then such provision will be deemed to be written, construed, and enforced as so limited. 

#### Amendment
AMENDMENT. This Contract may be modified or amended in writing by mutual agreement between the parties, if the writing is signed by the party obligated under the amendment. 

#### Governing Law
GOVERNING LAW. This Contract shall be construed in accordance with the Maxims of Equity. 

#### Notice
NOTICE. Any notice or communication required or permitted under this Contract shall be sufficiently given if delivered to a verifiable email address or to such other email address as one party may have publicly furnished in writing, or published on a broadcast contract provided by this blockchain for purposes of providing notices of this type. 
  
#### Waiver of Contractual Right
WAIVER OF CONTRACTUAL RIGHT. The failure of either party to enforce any provision of this Contract shall not be construed as a waiver or limitation of that party's right to subsequently enforce and compel strict compliance with every provision of this Contract. 

#### Arbitrator's Fees to Prevailing Party
ARBITRATOR’S FEES TO PREVAILING PARTY. In any action arising hereunder or any separate action pertaining to the validity of this Agreement, both sides shall pay half the initial cost of arbitration, and the prevailing party shall be awarded reasonable arbitrator's fees and costs.
  
#### Construction and Interpretation
CONSTRUCTION AND INTERPRETATION. The rule requiring construction or interpretation against the drafter is waived. The document shall be deemed as if it were drafted by both parties in a mutual effort. 
  
#### In Witness Whereof
IN WITNESS WHEREOF, the parties hereto have caused this Agreement to be executed by themselves or their duly authorized representatives as of the date of execution, and authorized as proven by the cryptographic signature on the transaction that invokes this contract.


