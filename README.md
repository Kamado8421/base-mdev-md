# 🤖 M'Dev Bot JS – Base Simples para WhatsApp

Bem-vindo à base oficial do **M'Dev Bot JS**, um projeto desenvolvido para facilitar a criação de bots no WhatsApp com JavaScript.
Ideal para desenvolvedores que desejam começar rápido com uma estrutura organizada, funcional e pronta para expandir.

---

## 🚀 Recursos Principais

- ✅ Estrutura modular e de fácil manutenção
- 💬 Envio e resposta de mensagens automáticas
- 📂 Suporte a comandos personalizados
- 🔒 Gerenciamento de sessões QR Code
- 📦 Pronto para deploy em ambientes como VPS ou localmente

---

````bash
npm install
````

Para resetar a conexão do bot, use:

```bash
npm run reset
npm run start # para nova conexão
```

## 📁 Estrutura do Projeto

- `assets/imagens` coloque aqui as imagens fixas do seu bot, como banners...
- `asssets/qrcode` aqui fica salvo a sessão do script com o whatsApp.
- `assets/cache` aqui fica salvo arquivos temporários que o script pode gerenciar e apagar automaticamente

Em `src/config/index.js` você deve ter a estrutura:

```javascript
const path = require('path');

const prefixo = '/'; // prefixo do bot
const nomeDono = 'MDev Systems'; // seu nome
const nomeBot = "M'Dev BOT"; // nome do bot
const numeroDono = "559900000000"; // numero do dono 55+DDD+NUMERO SEM O 9

const isMostrarQrcode = true; // se for true, ele vai mostrar o qrcode para conexão
const fazerBotResponderSomenteDono = false; // se for true, é ideal pra quando o bot tá em testes, só vai tesponder mensagens do dono.

// configuraçã de pastas (só mexa se necessário)
const pastaParaSalvarSessao = path.resolve(__dirname, '..', '..', 'assets', 'qrcode');
const pastaDeImagens = (arquivo) => path.resolve(__dirname, '..', '..', 'assets', 'images', `${arquivo}`);
const pastaTemporaria = path.resolve(__dirname, '..', '..', 'assets','cache');

module.exports = {
     prefixo,
     nomeBot,
     nomeDono,
     isMostrarQrcode,
     numeroDono,
     pastaParaSalvarSessao,
     pastaDeImagens,
     pastaTemporaria,
     fazerBotResponderSomenteDono,
}
```

**Obs:** sem as informações de `numeroDono` você não será identificado pelo bot como dono.

## Funções na `src/index.js`

```javascript
// envie mensagens de textos comum
const enviar = async (text) => {
  await mdevbot.sendMessage(from, { text }, { quoted: msg });
}

// use:
enviar('sua msg')

// envia imagens com ou sem legendas a partir de links de imagens online
const enviarImagemViaURL = async (url, legenda = '') => {
  await mdevbot.sendMessage(from, { image: { url }, caption: legenda }, { quoted: msg });
}

// use:
const url = 'link da sua imagem';
enviarImagemViaURL(url) // sem legenda
enviarImagemViaURL(url, "sua legenda") // com legenda

// envia imagens com ou sem legendas que estão armazenas em alguma pasta (images, cache ou outras)
const enviarImagemDePasta = async (rotaDoAquirvo, legenda = '') => {
  await mdevbot.sendMessage(from, { image: fs.readFileSync(rotaDoAquirvo), caption: legenda }, { quoted: msg });
}

// use: 
const rotaDoarquivo = '../assstes/imagens/banner.png' // caminho do arquivo
enviarImagemDePasta(rotaDoarquivo)
```
