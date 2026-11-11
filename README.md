# Marketplace Simplificado

Aplicação Django para catálogo público, carrinho em sessão, checkout com controle de estoque, API REST e administração de produtos por vendedor.

## Requisitos

- Python 3.12 ou superior
- Dependências listadas em `requirements.txt`

## Executar localmente

No Windows PowerShell:

```powershell
py -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

O catálogo fica em `http://127.0.0.1:8000/` e a administração em `/admin/`.
Cadastre categorias e produtos no Admin. Vendedores com acesso ao Admin só
visualizam e alteram os próprios produtos.

## API

- `GET /api/produtos/`: lista pública de produtos.
- `GET /api/produtos/?categoria=1&preco_min=10&preco_max=100`: filtra por categoria e faixa de preço.
- `GET /api/pedidos/`: lista os pedidos do usuário autenticado.
- `POST /api/pedidos/`: cria um pedido para o usuário autenticado.

Exemplo de corpo para criar um pedido:

```json
{
  "itens": [
    {"produto": 1, "quantidade": 2}
  ]
}
```

O preço é lido do cadastro do produto, nunca do cliente. O estoque é validado
antes de cada compra; pedido, itens e baixa de estoque acontecem em uma única
transação. A API navegável e o login estão disponíveis em `/api-auth/login/`.

## Testes

```powershell
python manage.py test
```
