Para testar o programa, usamos os arquivos hex que estão na pasta ROM&RAM. Tivemos bastante dificuldade para gerar arquivos que fossem aceitos adequadamente pelo programa, mas conseguimos por fim usando um script em python(checksum.py), que está na pasta dos hex.

Como explicado no relatório, os códigos de algumas operações são arbitrários. Abaixo, estão relacionados:

###
EXTENSÃO VETORIAL PERSONALIZADA
   - Opcode escolhido: 7'b0100111
   - Por que: É um opcode reservado na especificação RISC-V, permitindo criar uma extensão personalizada sem conflitar com instruções padrão. Instruções Vetoriais Personalizadas
- vadd.8  rd, rs1, rs2  (funct3=000)
- vadd.16 rd, rs1, rs2  (funct3=001)
- vsub.8  rd, rs1, rs2  (funct3=010)
- vsub.16 rd, rs1, rs2  (funct3=011)
- vand.8  rd, rs1, rs2  (funct3=100)
- vand.16 rd, rs1, rs2  (funct3=101)
- vor.8   rd, rs1, rs2  (funct3=110)
- vor.16  rd, rs1, rs2  (funct3=111)
###

###
CODIFICAÇÃO DA ALU (alu_ctrl[5:0])
   Bits [5:4]: Modo de operação
     00 = Escalar (32-bit)
     01 = 4 elementos de 8-bit
     10 = 2 elementos de 16-bit
     11 = Reservado
   Bits [3:0]: Operação específica
     0000 = ADD / vadd
     0001 = SUB / vsub
     0010 = AND / vand
     0011 = OR / vor
     0100 = XOR
     0101 = SLL
     0110 = SRL
     0111 = SRA
     1000 = LUI (passa imediato)
###


observação importante:
A ROM do Digital aparentemente recebe endereço de palavras. Depois de diversos testes e debugs, a escolha foi simplesmente escolher a parte maior de PC, ou seja 11:2. Assim, mantem-se a lógica próxima a um processador comum, que o endereçamento é por byte, com uma adaptação mínima para leitura.