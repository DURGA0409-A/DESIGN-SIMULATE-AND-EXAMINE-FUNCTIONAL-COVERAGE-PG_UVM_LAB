# DESIGN-SIMULATE-AND-EXAMINE-FUNCTIONAL-COVERAGE-PG_UVM_LAB
## EXPERIMENT – 6 DESIGN, SIMULATE AND EXAMINE FUNCTIONAL COVERAGE
## AIM
To design and simulate functional coverage using UVM and examine coverage results using Synopsys VCS.
## SOFTWARE REQUIRED
•	Synopsys VCS 
•	UVM Library 
•	Verdi (Optional) 
## THEORY
Functional coverage is used to measure how effectively the design functionality is verified.
In UVM:
•	Coverage is collected using covergroups. 
•	Transactions are sampled by monitor or subscriber. 
•	Coverage percentage indicates verification completeness. 
## Advantages:
•	Identifies untested cases 
•	Improves verification quality 
•	Helps achieve coverage goals 
## PROGRAM
UVM Functional Coverage (exp6.sv)
`include "uvm_macros.svh"
import uvm_pkg::*;
```
class transaction extends uvm_sequence_item;

  rand bit [1:0] a;

  `uvm_object_utils(transaction)

  covergroup cg;
    coverpoint a {
      bins low  = {0};
      bins mid  = {1,2};
      bins high = {3};
    }
  endgroup

  function new(string name="transaction");
    super.new(name);
    cg = new();
  endfunction

endclass


module test;

  transaction tr;

  initial begin

    tr = new();

    repeat(10) begin

      tr.randomize();

      $display("a = %0d", tr.a);

      tr.cg.sample();

    end

    $display("Coverage = %0.2f %%", tr.cg.get_coverage());

    $finish;

  end

endmodule
```
COMPILATION
vcs -sverilog -ntb_opts uvm exp6.sv -o simv
./simv
## RESULT
Thus, functional coverage using UVM was designed and simulated successfully.



