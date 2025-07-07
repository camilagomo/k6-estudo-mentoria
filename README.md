# Testes de Perfomance com K6
Este repositório contém um exemplo simples de teste de performance utilizando o [K6](https://k6.io/), uma ferramenta poderosa para testes de carga (load testing) e desempenho de APIs.

## 📦 Requisitos

- Node.js (opcional, mas recomendado)
- Acesso ao terminal/console
- [k6 instalado](#-instalação-do-k6)

---

## Instalação do K6

### Windows (via Chocolatey)

```bash
choco install k6
```

### MacOS (via Homebrew)

```bash
brew install k6
```

### Linux (via pacote .deb)

```bash
curl -s https://packagecloud.io/install/repositories/loadimpact/k6/script.deb.sh | sudo bash
sudo apt install k6
```

Para outros métodos de instalação, acesse: https://k6.io/docs/getting-started/installation/

---

## Primeiro Teste: Requisição POST

Crie um arquivo chamado `teste-login.js` com o seguinte conteúdo:

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  // Define o número de iterações
  iterations: 10,
};

export default function () {
  const url = 'http://localhost:3000/login';
  const payload = JSON.stringify({
    username: 'julio.lima',
    senha: '123456',
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  http.post(url, payload, params);
  sleep(1); // Espera 1 segundo entre as execuções
}
```

---

## ▶️ Executando o Teste

Com o K6 instalado e o servidor rodando localmente na porta 3000, execute o teste com o comando:

```bash
k6 run teste-login.js
```

Você verá um relatório no terminal com métricas como:
- Taxa de sucesso das requisições
- Tempo de resposta
- Número de iterações
- Erros (se houver)

---

## 📈 Exemplos de Métricas

Ao final do teste, você verá algo como:

```
http_req_duration......: avg=120ms  min=100ms  max=150ms
http_reqs..............: 10
vus....................: 1
iterations.............: 10
```
---

## 📚 Documentação oficial

Confira mais em: [https://k6.io/docs](https://k6.io/docs)

---

## ✨ Autor

Camila Monteiro – QA Engineer 💻


