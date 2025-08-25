# banco_DIO

import json
from decimal import Decimal, InvalidOperation
import os

# Constantes
LIMITE_SAQUES = 3
LIMITE_VALOR_SAQUE = 500

# Carregar dados salvos (se existirem)
def carregar_dados():
    try:
        if os.path.exists("dados.json") and os.path.getsize("dados.json") > 0:
            with open("dados.json", "r") as f:
                dados = json.load(f)
                # Convert saldo back to Decimal after loading
                dados["saldo"] = Decimal(dados["saldo"])
                return dados
        else:
            return {"saldo": Decimal(0), "extrato": [], "saques_hoje": 0}
    except (FileNotFoundError, json.JSONDecodeError) as e:
        print(f"Erro ao carregar dados: {e}")
        print("Inicializando dados padrão.")
        return {"saldo": Decimal(0), "extrato": [], "saques_hoje": 0}

# Salvar dados
def salvar_dados(saldo, extrato, saques_hoje):
    # Convert Decimal saldo to string before saving
    dados = {"saldo": str(saldo), "extrato": extrato, "saques_hoje": saques_hoje}
    with open("dados.json", "w") as f:
        json.dump(dados, f)

# Funções de operações
def depositar(saldo, extrato):
    try:
        valor_str = input("Valor do depósito: R$ ").replace(',', '.')
        valor = Decimal(valor_str)
        if valor <= 0:
            print("Valor deve ser positivo!")
            return saldo, extrato
        saldo += valor
        extrato.append(f"Depósito: R$ {valor:.2f}")
        print("Depósito realizado!")
        return saldo, extrato
    except (ValueError, InvalidOperation):
        print("Erro: Valor inválido!")
        return saldo, extrato

def sacar(saldo, extrato, saques_hoje):
    try:
        valor_str = input("Valor do saque: R$ ").replace(',', '.')
        valor = Decimal(valor_str)
        if valor <= 0:
            print("Valor deve ser positivo!")
            return saldo, extrato, saques_hoje
        if saques_hoje >= LIMITE_SAQUES:
            print("Limite de saques diários excedido!")
            return saldo, extrato, saques_hoje
        if valor > LIMITE_VALOR_SAQUE:
            print(f"Limite por saque: R$ {LIMITE_VALOR_SAQUE:.2f}")
            return saldo, extrato, saques_hoje
        if valor > saldo:
            print("Saldo insuficiente!")
            return saldo, extrato, saques_hoje
        saldo -= valor
        extrato.append(f"Saque: R$ {valor:.2f}")
        saques_hoje += 1
        print("Saque realizado!")
        return saldo, extrato, saques_hoje
    except (ValueError, InvalidOperation):
        print("Erro: Valor inválido!")
        return saldo, extrato, saques_hoje

def exibir_extrato(saldo, extrato):
    print("\n=============== EXTRATO ===============")
    if not extrato:
        print("Nenhuma movimentação.")
    else:
        for movimento in extrato:
            print(movimento)
    print(f"\nSaldo: R$ {saldo:.2f}")
    print("=======================================")

# Menu interativo
def main():
    dados = carregar_dados()
    saldo, extrato, saques_hoje = dados["saldo"], dados["extrato"], dados["saques_hoje"]

    while True:
        opcao = input("""
[d] Depositar
[s] Sacar
[e] Extrato
[q] Sair
=> """).strip().lower()

        if opcao == "d":
            saldo, extrato = depositar(saldo, extrato)
        elif opcao == "s":
            saldo, extrato, saques_hoje = sacar(saldo, extrato, saques_hoje)
        elif opcao == "e":
            exibir_extrato(saldo, extrato)
        elif opcao == "q":
            salvar_dados(saldo, extrato, saques_hoje)
            print("Saindo... Dados salvos!")
            break
        else:
            print("Opção inválida!")

if __name__ == "__main__":
    main()
