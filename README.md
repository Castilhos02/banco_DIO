Claro, Douglas! Aqui está um arquivo `README.md` completo e bem estruturado para acompanhar seu projeto no GitHub:

---

```markdown
# 💰 Sistema Bancário em Python

Este projeto é um sistema bancário simples desenvolvido em Python, que permite ao usuário realizar depósitos, saques, consultar extrato e salvar os dados em um arquivo local (`dados.json`). Ele simula o funcionamento básico de uma conta corrente com controle de limite de saques e persistência de dados entre sessões.

---

## 📦 Funcionalidades

- [x] Depósito com validação de valor
- [x] Saque com limite por operação (R$500)
- [x] Limite de 3 saques por sessão
- [x] Consulta de extrato com histórico de movimentações
- [x] Persistência de dados em JSON
- [x] Validação robusta de entrada e estrutura de dados

---

## 🧠 Como funciona

Ao iniciar o programa, ele tenta carregar os dados salvos no arquivo `dados.json`. Se o arquivo estiver ausente ou corrompido, os dados são inicializados com valores padrão.

O usuário interage com o sistema por meio de um menu de opções:

```text
[d] Depositar
[s] Sacar
[e] Extrato
[q] Sair
```

Cada operação é validada para garantir integridade e segurança dos dados.

---

## 🛠️ Requisitos

- Python 3.8 ou superior
- Biblioteca padrão (`json`, `decimal`, `os`)

---

## 🚀 Executando o projeto

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/sistema-bancario-python.git
cd sistema-bancario-python
```

2. Execute o script:

```bash
python banco.py
```

> Certifique-se de que o arquivo `dados.json` esteja no mesmo diretório ou será criado automaticamente.

---

## 📁 Estrutura de arquivos

```plaintext
sistema-bancario-python/
├── banco.py           # Script principal
├── dados.json         # Arquivo de dados persistentes (gerado automaticamente)
└── README.md          # Documentação do projeto
```

---

## 🔐 Validação de dados

O sistema trata os seguintes erros:
- Entrada não numérica ou inválida
- Valores negativos ou zero
- Saques acima do saldo ou do limite permitido
- Excesso de saques por sessão
- Estrutura corrompida ou ausente no arquivo JSON

---

## 📌 Observações

- O saldo é armazenado como `Decimal` para garantir precisão financeira.
- O extrato é mantido como uma lista de strings com descrição das movimentações.
- O sistema é ideal para fins didáticos e pode ser expandido com autenticação, múltiplos usuários ou interface gráfica.

---

## 📜 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

---

## 🙋 Autor

**Douglas Castilho**  
Aluno de Bacharelado em Tecnologia da Informação – UNIVESP  
São Paulo, Brasil
```
