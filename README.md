# Trilha Guiada — Entrega do Projeto Inicial da Rede

## Vozes do Quilombo — Rede da Casa Griô

**Maria do Carmo Barboza**  
**Equipe Tambor Digital**  
**Técnico em Informática — Módulo 2**  
**17 de julho de 2026**

---

## Identificação

| Campo | Resposta da equipe |
|---|---|
| **Nome da equipe** | Equipe Tambor Digital |
| **Integrante** | Maria do Carmo Barboza |
| **Turma** | Técnico em Informática - Módulo 2 |
| **Nome do projeto** | Vozes do Quilombo - Rede da Casa Griô |
| **Data** | 17 de julho de 2026 |

---

# 1. Missão

### Cenário pela equipe

> Utilizaremos o cenário adaptado: **Casa Griô de Cultura e Biblioteca Ancestral Quilombola**, com foco em criar a infraestrutura para o funcionamento do **Acervo Digital de Histórias Orais e Cantigas de Capoeira do Território de Itapecuru.**

---
## 2. Visao Geral e Cenario Atual da Casa Griô

A Casa Griô de Cultura e Biblioteca Ancestral Quilombola fica no Territorio de Itapecuru. Hoje a casa tem um roteador domestico simples que atende tudo junto, sem separacao de rede. O sinal do Wi-Fi nao chega no Barracao Cultural por causa das paredes de taipa. O servidor do Acervo Oral fica em um PC comum sem IP fixo, por isso vive caindo quando muitos celulares conectam. Nao ha rack, patch panel ou identificacao de cabos.

| Situacao Atual | Problema Encontrado |
| --- | --- |
| Internet | Link unico sem backup, sem firewall |
| Wi-Fi | Um SSID aberto para todos, sem senha diferente para visitantes |
| Cabeamento | Cabos soltos sem conduíte, sem padrao Cat6 |
| Energia | Sem nobreak para manter o servidor ligado |

## 3. Objetivos da Rede Vozes do Quilombo

| Tipo | Objetivo |
| --- | --- |
| Geral | Criar uma rede hierarquica, segura e estavel para guardar e divulgar as historias orais e cantigas de capoeira |
| Especifico 1 | Organizar o cabeamento estruturado com dois switches em cascata e garantir 1 Gbps no telecentro |
| Especifico 2 | Separar rede interna da rede de visitantes com dois SSIDs e futuras VLANs para proteger os saberes ancestrais |
| Especifico 3 | Garantir que o Servidor do Acervo Oral tenha IP fixo e acesso rapido para mestres e jovens |
| Especifico 4 | Deixar a rede pronta para oficinas de letramento digital com 20 PCs simultaneos |

## 4. Requisitos Tecnicos e Restricoes

| Requisito | Descricao | Prioridade |
| --- | --- | --- |
| Desempenho | Rede cabeada Gigabit para edicao de audios e videos do acervo | Alta |
| Seguranca | Isolamento logico entre Coordenacao e Visitantes | Alta |
| Disponibilidade | Servidor do Acervo no ar mesmo com queda de internet | Alta |
| Custo | Usar no maximo 2 switches, 2 APs e 1 caixa de cabo por ser projeto comunitario | Media |
| Distancia | Nenhum lance de cabo pode passar de 90 metros por causa do limite do UTP | Alta |
| Manutencao | Rede simples que possa ser mantida pela propria coordenacao sem equipe de TI externa | Alta |
| Ambiente | Equipamentos em local ventilado, fechado e protegido de poeira e calor da palha e taipa | Media |

# PARTE A — Compreensão do problema

## 5. Escreva o problema

### Problema formulado pela equipe

> Na Casa Griô de Cultura e Biblioteca Ancestral, mestres griôs, jovens, visitantes e a coordenação precisam gravar, ouvir e compartilhar o Acervo Digital de Histórias Orais e Cantigas, além de fazer oficinas de letramento digital, mas a casa não possui cabeamento estruturado, internet confiável e divisão entre rede pública e privada, o que deixa o servidor do acervo instável, dificulta o trabalho da coordenação e expõe os registros ancestrais a acessos indevidos de quem está de visita.

---

## 6. Identificar os usuários

| Grupo de usuários | Quantidade estimada | O que fazer na rede | Prioridade |
|---|---:|---|---|
| Coordenação / TI | 2 | Cuidar do servidor do acervo, da rede e dar suporte | Alta |
| Mestres Griôs / Oficineiros | 6 | Gravar áudios e vídeos e atualizar o acervo pelo Wi-Fi | Alta |
| Visitantes / Comunidade | 35 | Consultar o acervo oral e usar internet no celular | Média |
| Jovens do Território | 25 | Usar os computadores do telecentro para editar e estudar | Alta |

### Quem administrará ou manterá a rede?

A manutenção será feita pela própria coordenação da Casa Griô, com apoio remoto do provedor quando houver falha no link.

---

## 7. Setores ou ambientes

| Setor ou ambiente | Usuários | Dispositivos previstos | Necessidades principais |
|---|---|---|---|
| **Coordenação** | Coordenação | 1 PC, 1 Impressora | Acesso privado a arquivos e impressão segura |
| **Telecentro Griô** | Jovens | 20 PCs cabeados | Conexão estável com o Servidor do Acervo e internet |
| **Barracão Cultural** | Visitantes e Mestres | Celulares e notebooks | Wi-Fi amplo com isolamento da rede interna |
| **Sala Técnica / CPD** | TI | Servidor do Acervo, Switches, Roteador | Local fechado, ventilado e com energia protegida |

### Ambientes, distâncias ou obstáculos

> É preciso levantar a planta da Casa Griô para verificar paredes de taipa e palha que bloqueiam Wi-Fi e medir a distância do Barracão até a Sala Técnica para garantir que o cabo não passe de 90 metros.

---

## 8. Lista de necessidades e serviços

| Usuário ou setor | Necessidade | Relacionado | Importância | Como saberemos que funciona? |
|---|---|---|---|---|
| Todos | Ouvir o Acervo Oral | Servidor web interno | Alta | Abrir a página do acervo em qualquer dispositivo |
| Coordenação | Imprimir atividades | Impressão em rede | Alta | Mandar uma página teste da coordenação para impressora |
| Telecentro e Wi-Fi | Usar internet externa | NAT / Roteamento | Alta | Abrir um site público no navegador |
| Visitantes | Usar celular | Wi-Fi Visitantes | Média | Conectar celular sem conseguir acessar o servidor interno |
| Coordenação | Configurar rede | SSH / HTTPS | Alta | Entrar na tela de configuração do switch |

---

# PARTE B — Proposta

## 9. Recursos selecionados

| Recurso | Quantidade inicial | Necessidade atendida | Justificativa | Dúvida ou premissa |
|---|---:|---|---|---|
| **Switch 24 portas** | 1 | Ligar PCs do Telecentro | Junta os 20 PCs do telecentro em um único ponto | Premissa: Gigabit |
| **Switch 8 portas** | 1 | Ligar CPD e Coordenação | Atende servidor, PC, impressora e roteador | Premissa: ligado por uplink no switch de 24 |
| **Roteador de Borda** | 1 | Ligar LAN com internet | Faz NAT e já faz papel de firewall básico | Tem firewall integrado? |
| **Ponto de Acesso** | 2 | Wi-Fi para mestres e visitantes | Cobre barracão e telecentro | Qual alcance real? |
| **Servidor Torre** | 1 | Guardar Acervo Oral | Guarda o site e banco de áudios do Griô | Premissa: IP fixo |
| **Cabo UTP Cat6** | 1 caixa 305 m | Cabeamento | Garante 1 Gbps estável | Premissa: distância <90 m |

---

## Cálculo de portas

| Switch | Conexões | Portas utilizadas | Portas livres |
|---|---|---:|---:|
| Switch 24 portas | 20 PCs + 1 AP + 1 uplink | 22 | 2 |
| Switch 8 portas | 1 PC + 1 impressora + 1 servidor + 1 roteador + 1 uplink | 5 | 3 |
| **Total** | | **27** | **5** |

> **Total de portas:** 32  
> **Portas utilizadas:** 27  
> **Portas livres:** 5

### Quem usa Wi-Fi?

**Mestres Griôs e Visitantes.**

### Quantidade de APs é final?

Não. É uma estimativa inicial. Será necessário realizar um **Site Survey** para verificar a atenuação das paredes e a quantidade de usuários simultâneos.

---

# 10. Perguntas em aberto

| Tipo | Pergunta / Premissa | Por que importa? | Como confirmar? |
|---|---|---|---|
| Pergunta | O provedor entrega fibra com ONT ou rádio? | Define se precisa de conversor | Ver contrato do provedor |
| Premissa | O Acervo Oral precisa ser visto de fora da Casa Griô? | Define se precisa liberar porta externa e DNS | Conversar com os mestres griôs |
| Pergunta | AP suporta 2 SSIDs com isolamento? | Essencial para separar visitantes da rede interna | Ver datasheet |

---

# PARTE C — Topologia Inicial

```mermaid
flowchart TD
    ISP["Provedor Internet"] --- ROUTER["Roteador de Borda"]
    ROUTER --- SW8["Switch 8 Portas - CPD Griô"]
    SW8 --- SRV["Servidor Acervo Oral Griô"]
    SW8 --- PCADM["PC Coordenação"]
    SW8 --- IMP["Impressora"]
    SW8 === SW24["Switch 24 Portas - Telecentro"]
    SW24 --- PCS["20 PCs Telecentro"]
    SW24 --- AP["AP - WiFi Griô / WiFi Visitantes"]
