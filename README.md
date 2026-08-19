# 🎲 ATELOS RPG - Sistema de Mesa Digital

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Firebase](https://img.shields.io/badge/firebase-%23039BE5.svg?style=for-the-badge&logo=firebase)

O **ATELOS RPG** é um sistema de mesa digital completo projetado para facilitar sessões de RPG online, especialmente para grupos que fazem transmissões (streams). O sistema funciona direto no navegador, contando com um painel exclusivo para o Mestre, fichas automatizadas para os jogadores e uma **HUD (Overlay)** em tempo real pronta para ser integrada no OBS Studio.

---

## ✨ Funcionalidades

### 🧙‍♂️ Painel do Mestre (Game Master)
* **Visão Global:** Acompanhe os status de todos os jogadores em tempo real (PV, Mana, Sanidade).
* **Controle de Turnos:** Marque de quem é o turno atual (com destaque visual na HUD da stream).
* **Edição Rápida e Descanso:** Altere os atributos vitais dos personagens na hora, ou aplique "Descanso Longo" (50% ou 100%) para todo o grupo com um clique.
* **Log de Ações:** Registro de todas as rolagens de dados, danos sofridos e movimentações financeiras para manter o controle do jogo.
* **Controle de Visibilidade:** Oculte ou revele as informações de um jogador específico na HUD.

### 🎮 Painel do Jogador
* **Ficha Automatizada:** Cálculos automáticos de atributos (PV Máximo baseado em Constituição/Nível, Mana baseada em Sabedoria, Sanidade baseada em Carisma).
* **Rolador de Dados Integrado:** Role qualquer dado (d4 a d100), aplique modificadores e defina a margem de acerto crítico. O resultado aparece na hora tanto para o jogador quanto na tela da stream.
* **Controle de Recursos:**
  * **❤️ Pontos de Vida:** Com suporte a sistema de "Overheal" (Vida Temporária).
  * **💧 Mana / Stamina:** Controle de recursos de habilidades.
  * **🧠 Sanidade / Estresse:** Ao sofrer níveis críticos de perda de sanidade, a HUD e o painel aplicam efeitos visuais de loucura no nome e barra do personagem.
* **Gestão de Inventário e Magias:** Tabelas para cadastrar ataques, bônus e dano, além de controle financeiro (Cobre, Prata, Ouro e Platina).

### 📺 HUD para Stream (OBS Studio)
* **Resolução Otimizada:** Feita para 1920x1080.
* **Tempo Real:** As atualizações feitas pelos jogadores ou pelo Mestre refletem imediatamente na tela.
* **Efeitos Visuais Dinâmicos:** 
  * Turno ativo (efeito *Pulse*).
  * Cura excessiva (*Overheal* em verde brilhante).
  * Perda de Sanidade (glitches, embaralhamento do nome e efeito *Deep Madness* visual).
* **Exibição de Dados:** Resultados das rolagens de dados aparecem por alguns segundos na HUD, na posição respectiva do jogador que rolou.

---

## 🛠️ Tecnologias Utilizadas

* **Front-end:** HTML, CSS (com CSS Variables e Grid Layout), JavaScript Vanilla.
* **Back-end/Database:** [Firebase Firestore](https://firebase.google.com/docs/firestore) para banco de dados em tempo real.
* **Autenticação:** Firebase Auth (Login Anônimo para simplificar a entrada dos jogadores).
* **Design/UI:** Paleta de cores *Dark Fantasy* com detalhes em Ouro (`#c9a227`) e Vermelho (`#d93a3a`), utilizando as fontes `Cinzel` e `Inter` (Google Fonts).

---

## 🚀 Como Instalar e Usar

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/SEU_USUARIO/atelos-rpg.git
   ```

2. **Configure o Firebase:**
   O código atual usa um banco de dados de exemplo. Para usar o seu próprio:
   * Crie um projeto no [Firebase Console](https://console.firebase.google.com/).
   * Habilite o **Firestore Database** e configure as regras (Rules) para leitura/escrita.
   * Habilite o **Authentication** com o provedor *Anônimo*.
   * Substitua a variável `firebaseConfig` no final do arquivo HTML com as credenciais do seu projeto:
     ```javascript
     const firebaseConfig = {
       apiKey: "SUA_API_KEY",
       authDomain: "SEU_DOMINIO.firebaseapp.com",
       projectId: "SEU_PROJECT_ID",
       storageBucket: "SEU_BUCKET.appspot.com",
       messagingSenderId: "SEU_SENDER_ID",
       appId: "SEU_APP_ID"
     };
     ```

3. **Hospedagem / Rodando Local:**
   * Por não usar frameworks pesados (apenas o CDN do Firebase), você pode simplesmente abrir o arquivo `index.html` em qualquer navegador.
   * Para partidas com amigos, hospede gratuitamente em serviços como [GitHub Pages](https://pages.github.com/), [Vercel](https://vercel.com/) ou [Netlify](https://www.netlify.com/).

4. **Adicionando a HUD no OBS:**
   * Crie uma nova **Fonte de Navegador** (Browser Source) no OBS Studio.
   * Insira a URL onde o sistema está hospedado.
   * Defina a largura para `1920` e a altura para `1080`.
   * Pelo painel (após o login de Mestre ou via URL), acesse a tela do HUD para capturar os dados.

---

## 📝 Regras do Firebase (Firestore) - Sugestão

Para que o aplicativo funcione corretamente com autenticação anônima, você pode usar a seguinte regra de segurança (apenas para testes; em produção recomenda-se validar o ID do usuário):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

---

## 📄 Licença

Este projeto é de código aberto e está disponível sob a licença MIT. Sinta-se à vontade para realizar *forks*, customizar regras de atributos e usar em suas mesas de RPG!
