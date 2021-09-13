# sistemabancario

import pickle
import os
import pathlib
class Conta :
    contacliente = 0
    contacliente1 = 0
    nome = ''
    deposit=0
    senha = 0 



    def criarConta(self):

        self.contacliente= int(input("Informe o número da conta do cliente com \n  5 digitos, e o primeiro deve ser maior que 0 "))
        if 10000 <= self.contacliente <= 99999:
            self.nome = input("Digite o nome completo do cliente: ")
            self.contacliente1 = input("Digite uma senha")
            if 5 <= len(self.contacliente1) <= 8:   
                self.telefone = int(input("Digite o telefone"))
                self.rendamensal = int(input("Digite a renda mensal do cliente"))
                self.profissao = input("digite a profissao do cliente")
                self.endereco = input("digite o endereço do cliente")
                self.deposit = int(input("Caso deseje realizar deposito insira, ou tecle 0"))
                print("\n\n\nCliente cadastrado")
            else:
                print("A senha deve conter de 4 a 8 algoritmos alfanumerericos")


        else:
            print("Não é possível cadastrar")



    
    def ModificarCadstro(self):
        print("Conta: ",self.contacliente)
        self.nome = input("nome :")
        self.contacliente1 = input("senha :")
        self.deposit = int(input("saldo :"))
        self.telefone = int(input("Digite o telefone"))
        self.rendamensal = int(input("Digite a renda mensal do cliente"))
        self.profissao = input("digite a profissao do cliente")
        self.endereco = input("digite o endereço do cliente")
        
    def Depositar(self,saldo):
        self.deposit += saldo
    
    def Sacar(self,saldo):
        self.deposit -= saldo
    
    def report(self):
        print(self.contacliente, " ",self.nome ," ",
         self.deposit," ", self.telefone," ", self.rendamensal," ", self.profissao," ", self.endereco, " ")
    
    def salvarconta(self):
        return self.contacliente
    def salvarnome(self):
        return self.nome
    def salvarsenha(self):
        return self.contacliente1
    def salvardeposito(self):
        return self.deposit
    def salvartelefone(self):
        return self.telefone
    def salvarrenda(self):
        return self.rendamensal
    def salvarprofissao(self):
        return self.profissao
    def salvarendereco(self):
        return self.endereco
    




def funcaocriarconta():
    conta = Conta()
    conta.criarConta()
    criarcontaarquivo(conta)

def funcaoclientescadastrados():
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        for item in Listagem :
            print("conta",item.contacliente," cliente", item.nome, " saldo",item.deposit, " telefone", item.telefone, " renda mensal",
            item.rendamensal, " profissão", item.profissao, "endereço ", item.endereco)
        bancodedados.close()
    else :
        print(" ")
        

def funcaoconsultarclientepelaconta(num): 
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        bancodedados.close()
        found = False
        for item in Listagem :
            if item.contacliente == num :
                print("conta",item.contacliente," cliente", item.nome, " saldo",item.deposit, " telefone", item.telefone, " renda mensal",
            item.rendamensal, " profissão", item.profissao, "endereço ", item.endereco, " " )
                found = True
    else :
        print("não consta no banco")
    if not found :
        print("Incorreto")


def depositAndWithdraw(num1,num2,senha): 
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        bancodedados.close()
        os.remove('criarcontanova.data')
        for item in Listagem :
            if item.contacliente == num1 and item.contacliente1 == senha:
                if num2 == 1 :
                    saldo = int(input("Digite o valor a ser depositado "))
                    if 0 <= saldo <= 10000:
                        item.deposit += saldo
                        print("O valor foi depositdado")
                    else:
                        print("o valor deve ser menor que 10000")
                elif num2 == 2 :
                    saldo = int(input("Digite quanto deseja sacar "))
                    if saldo <= item.deposit :
                        item.deposit -=saldo
                    else :
                        print("Você não possui essa quantidade")
            else:
                print(" ")

    else :
        print(" ")
    bancodedadoscadastro = open('contacriada.data','wb')
    pickle.dump(Listagem, bancodedadoscadastro)
    bancodedadoscadastro.close()
    os.rename('contacriada.data', 'criarcontanova.data')

def funcaoinvestimento(num,senha): 
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        bancodedados.close()
        found = False
        for item in Listagem :
            if item.contacliente == num and item.contacliente1 == senha:
                meses = int(input("Insira o numero de meses:\n"))
                aplicacao = int(input("digite a aplicaçao mensal"))
                for mes in range(1, meses + 1):
                    saldo = aplicacao + (item.deposit * 1.015)
                    if mes % 12 == 0:
                        if meses >= 60:
                            saldo = aplicacao - (item.deposit * 0.005)
                            found = True
                            print(round(saldo, 2))
                        else:
                            saldo = aplicacao - (item.deposit * 0.01)
                            print(round(saldo, 2))
                if meses < 12:
                    saldo = saldo - (saldo * 0.01)
                    print(round(saldo, 2))
                else:
                    print(" ")

    else :
        print("Não consta")

def deleteAccount(num):
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        listaantigabancodedados = pickle.load(bancodedados)
        bancodedados.close()
        novalistagem = []
        for item in listaantigabancodedados :
            if item.contacliente != num :
                novalistagem.append(item)
        os.remove('criarcontanova.data')
        bancodedadoscadastro = open('contacriada.data','wb')
        pickle.dump(novalistagem, bancodedadoscadastro)
        bancodedadoscadastro.close()
        os.rename('contacriada.data', 'criarcontanova.data')
     
def ModificarCadstro(num):
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        listaantigabancodedados = pickle.load(bancodedados)
        bancodedados.close()
        os.remove('criarcontanova.data')
        for item in listaantigabancodedados :
            if item.contacliente == num :
                num = input("digite a conta do cliente")
                novasenha = input("digite a senha anterior para cadastrar uma nova")
                if novasenha == item.contacliente1 and len(novasenha) == 5 :

                  item.contacliente1 = input("Digite a nova senha")
                  item.telefone = int(input("digite o novo telefone"))
                  item.renamensal = int(input("digite a nova renda"))
                  item.profissao = input("digte a nova profissao")
                else:
                  print("incorreto")
        bancodedadoscadastro = open('contacriada.data','wb')
        pickle.dump(listaantigabancodedados, bancodedadoscadastro)
        bancodedadoscadastro.close()
        os.rename('contacriada.data', 'criarcontanova.data')


   

def criarcontaarquivo(conta) : 
    
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        listaantigabancodedados = pickle.load(bancodedados)
        listaantigabancodedados.append(conta)
        bancodedados.close()
        os.remove('criarcontanova.data')
    else :
        listaantigabancodedados = [conta]
    bancodedadoscadastro = open('contacriada.data','wb')
    pickle.dump(listaantigabancodedados, bancodedadoscadastro)
    bancodedadoscadastro.close()
    os.rename('contacriada.data', 'criarcontanova.data')

def funcaoconsultarnome(consultarnomecliente):

    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        bancodedados.close()
        found = False
        for item in Listagem :
            if item.nome == consultarnomecliente :
                print("conta",item.contacliente," cliente", item.nome, " saldo",item.deposit, " telefone", item.telefone, " renda mensal",
            item.rendamensal, " profissão", item.profissao, "endereço ", item.endereco, " " )
                found = True
    else :
        print("Não consta  ")
    if not found :
        print("Não consta")

def funcaoextrato(num,senha):
    consultarbanco = pathlib.Path("criarcontanova.data")
    if consultarbanco.exists ():
        bancodedados = open('criarcontanova.data','rb')
        Listagem = pickle.load(bancodedados)
        bancodedados.close()
        found = False
        for item in Listagem :
            if item.contacliente == num and item.contacliente1 :
                print('-' * 30)
                print('        EXTRATO DE {}      '.format(item.nome))
                print('-' * 30)
                print('BANCO - ADM')
                print('CONTA {} --- TELEFONE {}'.format((item.contacliente), (item.telefone)))
                print('-' * 30)
                print('-' * 30)
                print('ULTIMOS LANCAMENTOS')
                print(' DEPÓSITO ATM |   PROFISSÃO {} '.format(item.profissao))
                print('              |                |')
                print('              |                |')
                print('-' * 30)
                print('                  SALDO: R$ {}'.format(item.deposit))
                print('-' * 30)
                print('        FIM DO EXTRATO	      ')
                print('-' * 30)
                aperte = input('Aperte ENTER para retornar ao MENU: ')
                print("conta",item.contacliente," cliente", item.nome, " saldo",item.deposit, " telefone", item.telefone, " renda mensal",
                    item.rendamensal, " profissão", item.profissao, "endereço ", item.endereco, " " )
                found = True
            else:
                print("incorreto")
    else :
        print("incorreto")
    if not found :
        print("incorreto")




        
consultarnomecliente=0
menu=''
num=0
senha=0
while menu != 8:

    print("Digite a opção desejada:")
    print("\t1 - Inserir cliente(ADM)")
    print("\t2 - Atualizar cadastro de um cliente(ADM)")
    print("\t3 - Remover algum cliente da lista(ADM)")
    print("\t4 - Consultar um cliente(ADM)")
    print("\t5 - Lista dos clientes cadastrados(ADM)")
    print("\t6 - Sacar da conta de cliente")
    print("\t7 - Depositar valor")
    print("\t8 - Consultar extrato")
    print("\t9 - Simular investimento")
    print("\t10 - Sair")
    menu = input()

    
    if menu == '1':
        ADM = input("Usuario")
        senha = int(input("senha"))
        if ADM == ('ADM') and senha == 123:
            funcaocriarconta()
        else:
          print("incorreto")
    elif menu =='7':
        num = int(input("\tInforme o número da conta do cliente:  "))
        senha = input("informe a senha")
        depositAndWithdraw(num, 1, senha)
    elif menu == '6':
        num = int(input("\tInforme o número da conta do cliente:  "))
        senha = int(input("informe a senha"))
        depositAndWithdraw(num, 2, senha)
    elif menu == '4':
        ADM = input("Usuario")
        senha = int(input("senha"))
        if ADM == ('ADM') and senha == 123:
            print("1 - consultar pelo nome")
            print("2 - consultar pela conta")
            opcaodeconsultar = input("digite a opcao desejada")
            if opcaodeconsultar == '1':
                consultarnomecliente = input("digite o nome do cliente")
                funcaoconsultarnome(consultarnomecliente)
            elif opcaodeconsultar == '2':
                num = int(input("\tInforme o número da conta do cliente:  "))
                funcaoconsultarclientepelaconta(num)
        else:
          print("incorreto")
    elif menu == '5':
        ADM = input("Usuario")
        senha = int(input("senha"))
        if ADM == ('ADM') and senha == 123:
          funcaoclientescadastrados()
        else:
          print("incorreto")
    elif menu == '3':
        ADM = input("Usuario")
        senha = int(input("senha"))
        if ADM == ('ADM') and senha == 123:
          num =int(input("\tInforme o número da conta do cliente:  "))
          deleteAccount(num)
        else:
          print("incorreto")

    elif menu == '2':
        ADM = input("Usuario")
        senha = int(input("senha"))
        if ADM == ('ADM') and senha == 123:
          num = int(input("\tInforme o número da conta do cliente:  "))
          ModificarCadstro(num)
        else:
          print("incorreto")
    elif menu == '8':
        num = int(input("Informe sua conta"))
        senha = input("informe a senha")
        funcaoextrato(num,senha)
    elif menu == '9':
        num = int(input("Informe a conta"))
        senha = input("Informe a senha")
        funcaoinvestimento(num,senha)
    elif menu == '10':
        print("\tSair")
        break


    else :
        print("Digite um valor válido")
    
    menu = input("Tecle Enter ")
    
