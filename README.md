# Entrega-do-projeto-inicial-da-rede-

Trilha guiada — Entrega do: projeto inicial da rede

Identificação
Campo	Resposta da equipe
Nome da equipe	Equipe Tambor Digital
Integrantes	Maria do Carmo Barboza
Turma	Técnico em Informática - Módulo 2
Nome do projeto	Vozes do Quilombo - Rede da Casa Griô
Data	17 de julho de 2026
1. Missão
Cenário pela equipe
Utilizaremos o cenário adaptado: Casa Griô de Cultura e Biblioteca Ancestral Quilombola, com foco em criar a infraestrutura para o funcionamento do Acervo Digital de Histórias Orais e Cantigas de Capoeira do Território de Itapecuru.

Parte A — Compreensão do problema

5. Escreva o problema
Problema formulado pela equipe
Na Casa Griô de Cultura e Biblioteca Ancestral, mestres griôs, jovens, visitantes e a coordenação precisam gravar, ouvir e compartilhar o Acervo Digital de Histórias Orais e Cantigas, além de fazer oficinas de letramento digital, mas a casa não possui cabeamento estruturado, internet confiável e divisão entre rede pública e privada, o que deixa o servidor do acervo instável, dificulta o trabalho da coordenação e expõe os registros ancestrais a acessos indevidos de quem está de visita.

6. Identificar os usuários
Grupo de usuários	Quantidade estimada	O que fazer na rede	Prioridade
Coordenação / TI	2	Cuidar do servidor do acervo, da rede e dar suporte	Alta
Mestres Griôs / Oficineiros	6	Gravar áudios e vídeos e atualizar o acervo pelo Wi-Fi	Alta
Visitantes / Comunidade	35	Consultar o acervo oral e usar internet no celular	Média
Jovens do Território	25	Usar os computadores do telecentro para editar e estudar	Alta
Quem administrará ou manterá a rede?
A manutenção será feita pela própria coordenação da Casa Griô, com apoio remoto do provedor quando houver falha no link.

7. Identifique os setores ou ambientes
Setor ou ambiente	Usuários tratados	dispositivos previstos	Necessidades principais
Coordenação	Coordenação	1 PC, 1 Impressora	Acesso privado a arquivos e impressão segura
Telecentro Griô	Jovens	20 PCs cabeados	Conexão estável com o Servidor do Acervo e internet
Barracão Cultural	Visitantes e Mestres	Celulares e notebooks	Wi-Fi amplo com isolamento da rede interna
Sala Técnica / CPD	TI	Servidor do Acervo, Switches, Roteador	Local fechado, ventilado e com energia protegida
Há ambientes, distâncias ou obstáculos que ainda precisam ser conhecidos?
Sim. É preciso levantar a planta da Casa Griô para verificar paredes de taipa e palha que bloqueiam Wi-Fi e medir a distância do Barracão até a Sala Técnica para garantir que o cabo não passe de 90 metros.

8. Lista de necessidades e serviços
Usuário ou setor	Necessidade	relacionado	Importância	Como saberemos que funciona?
Todos	Ouvir o Acervo Oral	Servidor web interno	Alta	Abrir a página do acervo em qualquer dispositivo
Coordenação	Imprimir atividades	Impressão em rede	Alta	Mandar uma página teste da coordenação para impressora
Telecentro e Wi-Fi	Usar internet externa	NAT / Roteamento	Alta	Abrir um site público no navegador
Visitantes	Usar celular	Wi-Fi Visitantes	Média	Conectar celular sem conseguir acessar o servidor interno
Coordenação	Configurar rede	SSH / HTTPS	Alta	Entrar na tela de configuração do switch
Parte B — Proposta

9. Selecione recursos e justifique
Recurso	Quantidade inicial	Necessidade atendida	Justificativa	Dúvida ou premissa
Switch 24 portas	1	Ligar PCs do Telecentro	Junta os 20 PCs do telecentro em um único ponto	Premissa: Gigabit
Switch 8 portas	1	Ligar CPD e Coordenação	Atende servidor, PC, impressora e roteador sem sobrar muito	Premissa: ligado por uplink no switch de 24
Roteador de Borda	1	Ligar LAN com internet	Faz NAT e já faz papel de firewall básico	Pergunta: tem firewall integrado?
Ponto de Acesso	2	Wi-Fi para mestres e visitantes	Cobre barracão e telecentro	Pergunta: qual alcance real?
Servidor Torre	1	Guardar Acervo Oral	Guarda o site e banco de áudios do Griô	Premissa: IP fixo
Cabo UTP Cat6	1 caixa 305m	Cabeamento	Garante 1 Gbps estável	Premissa: distância <90m
Cálculo de portas:
Conexões cabeadas iniciais: 24 (20 PCs telecentro + 1 PC coordenação + 1 impressora + 1 servidor + 1 AP)
Portas livres: 5

A conta: Switch 24 portas: 20 PCs + 1 AP + 1 uplink = 22 usadas, sobram 2. Switch 8 portas: 1 PC coordenação + 1 impressora + 1 servidor + 1 roteador + 1 uplink = 5 usadas, sobram 3. Total 32 - 27 = 5 livres para futuro.

Quem usa Wi-Fi? Mestres Griôs e Visitantes.
Quantidade de APs é final? Não, é estimativa inicial. Precisa de Site Survey para ver atenuação das paredes e quantos usuários simultâneos.

10. Perguntas em aberto
Tipo	Pergunta/Premissa	Por que importa?	Como confirmar?
Pergunta	O provedor entrega fibra com ONT ou rádio?	Define se precisa de conversor	Ver contrato do provedor
Premissa	O Acervo Oral precisa ser visto de fora da Casa Griô?	Define se precisa liberar porta externa e DNS	Conversar com os mestres griôs
Pergunta	AP suporta 2 SSIDs com isolamento?	Essencial para separar visitantes da rede interna	Ver datasheet
Parte C — Topologia inicial

11. Desenhe a topologia
flowchart TD
    ISP["Provedor Internet"] --- ROUTER["Roteador de Borda"]
    ROUTER --- SW8["Switch 8 Portas - CPD Griô"]
    SW8 --- SRV["Servidor Acervo Oral Griô"]
    SW8 --- PCADM["PC Coordenação"]
    SW8 --- IMP["Impressora"]
    SW8 === SW24["Switch 24 Portas - Telecentro"]
    SW24 --- PCS["20 PCs Telecentro"]
    SW24 --- AP["AP - WiFi Griô / WiFi Visitantes"]
Leitura da topologia:
Tráfego entra e sai só pelo roteador. Switch de 8 portas no CPD é o centro. Servidor do Acervo Oral fica direto nele para ter mais velocidade. Wi-Fi entra pelo AP que joga para o switch do telecentro. Falta no desenho: VLANs para isolar visitantes, controle de banda e ACLs de firewall.

12. Checklist técnico
Corrigimos o AP que antes estava no roteador e agora está no switch para manter hierarquia de camada 2 correta.

Parte E — Revisão

18. Uso de IA
Ferramenta: Gemini 
Aceita: ideia de usar 2 switches em cascata separando telecentro e CPD
Rejeitada: OSPF, rede é pequena e estática
Verificação: conferimos com apostila de cabeamento estruturado
Correção: redistribuímos portas livres

19. Justificativa
O projeto Vozes do Quilombo atende a Casa Griô com uma rede hierárquica simples e segura. Separar em dois switches organiza o cabeamento e isola o telecentro da coordenação. O servidor do Acervo Oral no switch central garante desempenho máximo. O roteador centraliza a internet e já deixa pronto para futuras VLANs que vão proteger os saberes ancestrais.

23. Síntese
Decisão principal: manter servidor do Acervo Oral no switch do CPD perto do roteador para otimizar acesso.
Maior dúvida: como configurar VLANs nos SSIDs para impedir que visitante acesse a coordenação.
Próxima aula: aprender sobre tabela MAC, ARP e criação de VLANs.
