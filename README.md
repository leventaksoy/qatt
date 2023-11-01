***** AIM *****
Aim of the qatt Perl code is to realize the query attack. 

***** USAGE *****
The usage of the qatt code can be given as follows which can be obtained after running the "perl qatt.pl -h" command:

Usage:       perl qatt.pl -ef=<FileName> -of=<FileName> -ox=<ExecFile> -pkf=<FileName> -p=<FileName> -sat=<int> -st=<int> -ss=<int> -qt=<int> -qn=<int> -eq -osw -con=helloctf/csaw19 -iter -iqn=0/1 -in=<int> -rt=<int> -v -h 
ef:          Name of the encrypted file in bench format                                                                                                                                                                        
of:          Name of the oracle file in bench format                                                                                                                                                                           
ox:          Name of the oracle executable                                                                                                                                                                                     
pkf:         Name of the file including the partial key                                                                                                                                                                        
p:           Name of the file including paths to the ATPG Atalanta tool and SAT solvers by default it is paths.pl under the same directory                                                                                     
sat:         SAT solver used for regular tasks by default it is CaDiCaL                                                                                                                                                        
               0: cryptominisat                                                                                                                                                                                                
               1: lingeling                                                                                                                                                                                                    
               2: plingeling - parallel                                                                                                                                                                                        
               3: glucose                                                                                                                                                                                                      
               4: CaDiCaL - incremental                                                                                                                                                                                        
st:          Run-time limit for the SAT solver in seconds by default it is 3600                                                                                                                                                
ss:          Seed for the randomness in a SAT solver by default it is 1                                                                                                                                                        
qt:          Technique for obtaining queries by default it is 3                                                                                                                                                                
               0: random                                                                                                                                                                                                       
               1: ATPG tool Atalanta targeting key bits                                                                                                                                                                        
               2: ATPG tool Atalanta targeting all wires                                                                                                                                                                       
               3: ATPG tool Atalanta targeting key inputs + random                                                                                                                                                             
qn:          Maximum number of queries to be considered by default it is twice of the number of key bits                                                                                                                       
eq:          Determine the relation of two key bits by default it does not                                                                                                                                                     
osw:         Assumes that the operating system is WINDOWS by default it does not                                                                                                                                               
con:         Name of the contest which provides the executable oracle by default it is helloctf                                                                                                                                
iter:        Runs the query attack iteratively by default it does not                                                                                                                                                          
iqn:         Technique that determines the number of queries in the iterative query attack by default it is 0                                                                                                                  
               0: static                                                                                                                                                                                                       
               1: dynamic - doubles if the last 3 attempts could not improve the number of proven keys                                                                                                                         
in:          Iteration number limit for the iterative query attack by default it is 1000                                                                                                                                       
rt:          Run-time limit for the iterative query attack in seconds by default it is 172800                                                                                                                                  
v:           Shows the process of the query attack by default it does not                                                                                                                                                      
h:           Prints this page                                                                                                                                                                                                  
Description: This code implements the query attack                                                                                                                                                                             
Examples:    perl qatt.pl ef=../examples/bench/c6288/c6288_xor120.bench -of=../examples/bench/c6288/c6288_norg.bench                                                                                                           
             perl qatt.pl ef=../examples/bench/c6288/c6288_xor120.bench -of=../examples/bench/c6288/c6288_norg.bench -sat=0 -qt=0 -qn=120 -v                                                                                   
             perl qatt.pl ef=../examples/bench/c2670/c2670_xor240.bench -of=../examples/bench/c2670/c2670.bench -iter -qt=0 -v                                                                                                 
             perl qatt.pl ef=../examples/csaw19/small/small_v2.bench -ox=../examples/csaw19/small/small.bench -con=csaw19 -v                                                                                                   

***** IO FILES *****
The oracle-guided query attack needs both oracle and encrypted circuits. While the oracle circuit can be a binary file or described in a bench file, the encrpted circuit should be described in a bench file. 
In the encrypted file, each key bit should start with the "keyinput" phrase and should be stated between the primary inputs and outputs of the original circuit.

***** DEPENDICES *****
The query attack requires the ATPG tool Atalanta and a SAT solver.

*** ATALANTA ***
The Atalanta ATPG tool can be obtained from https://github.com/hsluoyz/Atalanta/. The installation is straight-forward. To prevent Atalanta tool to print unnecassary information on the screen such as "before", "after", or "end initialazition"
the related commands in the codes can be commented.

*** SAT SOLVER ***
The query attack currently supports 5 SAT solvers, namely cryptominisat, lingeling, plingeling, glucose, and CaDiCaL. They can be obtained from the sites given below. The query attack prefers CaDiCaL.
Cryptominisat: https://www.msoos.org/cryptominisat5/
Lingeling, Plingeling: http://fmv.jku.at/lingeling/
Glucose: https://www.labri.fr/perso/lsimon/research/glucose/
CaDiCaL: http://fmv.jku.at/cadical/

After these ATPG tool and a SAT solver are installed, their paths should be given in a file. Please check the "paths.pl" file as an example.

The query attack was tested under Windows 10 using the Strawberry Perl (https://strawberryperl.com/) and under Linux running Perl v5.26.1.

***** CONTACT *****
Please contact Levent Aksoy (leventaksoy@taltech.ee) if you have any trouble running the code and suggestions and/or comments.
