# pdb2src

PDB2SRC is a comprehensive dia2dump modification created in an evening to
generate a detailed PDB source tree representation. When provided with a PDB
file (including Xbox (XEX) ones, as they are compatible), it first extracts the
source code layout. Then, it proceeds to extract each function's signature and
map them to their respective source files. The line number information
available in the PDB is used to accurately deduce the function hierarchy, as it
originally existed.

NOTE: The code quality is awful, leaky, and potentially dangerous as this project
was nothing more than an ad-hoc solution created using available resources to
meet an immediate need. This is also recovered from drive, so it probably
doesn't compile anymore.


![Screenshot from 2023-10-10 22-33-27](Screenshot%20from%202023-10-10%2022-33-27.png)
