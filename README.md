# Lista para armazenar usuários
usuarios = []
# Lista para armazenar contas
contas = []

def criar_usuario(nome, data_nascimento, cpf, endereco):
    # Verifica se o CPF já existe
    for usuario in usuarios:
        if usuario['cpf'] == cpf:
            print("CPF já cadastrado.")
            return
    # Adiciona usuário
    usuarios.append({
        'nome': nome,
        'data_nascimento': data_nascimento,
        'cpf': cpf,
        'endereco': endereco
    })
    print(f"Usuário {nome} cadastrado com sucesso.")

def criar_conta(agencia, usuario_cpf):
    # Verifica se o usuário existe
    for usuario in usuarios:
        if usuario['cpf'] == usuario_cpf:
            numero_conta = len(contas) + 1  # Conta começa em 1
            contas.append({
                'agencia': agencia,
                'numero_conta': numero_conta,
                'usuario': usuario
            })
            print(f"Conta {numero_conta} criada para {usuario['nome']}.")
            return
    print("Usuário não encontrado.")

def deposito(saldo, valor, extrato):
    saldo += valor
    extrato.append(f'Depósito: R$ {valor:.2f}')
    return saldo, extrato

def saque(*, saldo, valor, extrato, limite, numero_saque, limite_saque):
    if numero_saque >= limite_saque:
        print("Limite de saques atingido.")
    elif valor > saldo:
        print("Saldo insuficiente.")
    else:
        saldo -= valor
        extrato.append(f'Saque: R$ {valor:.2f}')
        numero_saque += 1
    return saldo, extrato

def visualizar_historico(extrato):
    for item in extrato:
        print(item)

# Exemplo de uso
criar_usuario('David', '01/01/2000', '12345678900', 'Rua A - Bairro B - Cidade C - SP')
criar_conta('0001', '12345678900')

saldo = 1000
extrato = []
saldo, extrato = deposito(saldo, 2000, extrato)
saldo, extrato = saque(saldo=saldo, valor=150, extrato=extrato, limite=500, numero_saque=0, limite_saque=3)
visualizar_historico(extrato)
