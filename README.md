# ATS11-GitActions

Este repositorio contem uma API Python com FastAPI e um pipeline de Integracao Continua (CI) configurado com GitHub Actions.

## Estrutura

- `main.py` - API FastAPI com rotas para leitura raiz, soma e multiplicacao.
- `test_main.py` - testes automatizados com `pytest` para validar as rotas.
- `.github/workflows/ci.yml` - workflow do GitHub Actions que executa testes e um teste de integracao.
- `requirements.txt` - dependencias do projeto.

## Como funciona o CI

O workflow `Teste de API` roda em duas situacoes:

- `push`
- `pull_request`

Ele executa o job `verificar-api` com matrix de Python:

- `3.10`
- `3.11`
- `3.12`

Passos do workflow:

1. Faz checkout do codigo.
2. Instala a versao de Python do matrix.
3. Instala dependencias via `requirements.txt`.
4. Roda `pytest test_main.py`.
5. Inicia a API em background com Uvicorn.
6. Verifica a rota raiz e a rota `/somar/10/20` com `curl`.

## Como testar localmente

1. Crie e ative seu ambiente virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\activate
```

2. Instale as dependencias:

```powershell
pip install -r requirements.txt
```

3. Rode os testes:

```powershell
pytest -q
```

4. Opcional: execute a API localmente:

```powershell
uvicorn main:app --reload
```

A API ficara disponivel em `http://127.0.0.1:8000`.

## Rotas disponiveis

- `GET /` - verifica se a API esta funcionando.
- `GET /somar/{a}/{b}` - soma dois numeros.
- `GET /multiplicar/{a}/{b}` - multiplica dois numeros.

## Observacoes

O pipeline foi configurado para proteger a branch `main` e garantir que o codigo so seja mesclado apos o sucesso dos testes.
