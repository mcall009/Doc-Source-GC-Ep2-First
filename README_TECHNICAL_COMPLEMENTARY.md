# Grand Chase Season V EP2 - Documentação Técnica Detalhada

## Sumário

1. [Estrutura da Source](#estrutura-da-source)
2. [Arquivos Principais](#arquivos-principais)
   - [Estrutura do Cliente](#estrutura-do-cliente)
   - [Estrutura do Servidor](#estrutura-do-servidor)
   - [Bibliotecas e Dependências](#bibliotecas-e-dependências)
3. [Guias de Implementação](#guias-de-implementação)
   - [Implementando Novos Personagens](#implementando-novos-personagens)
   - [Adicionando Novas Armas e Itens](#adicionando-novas-armas-e-itens)
   - [Criando Novos Dungeons e Mapas](#criando-novos-dungeons-e-mapas)
   - [Implementando Novos Eventos](#implementando-novos-eventos)
   - [Adicionando Novos Efeitos Visuais](#adicionando-novos-efeitos-visuais)
4. [Correções e Otimizações](#correções-e-otimizações)
   - [Problemas Conhecidos](#problemas-conhecidos)
   - [Bugs Críticos](#bugs-críticos)
   - [Otimizações Recomendadas](#otimizações-recomendadas)
   - [Melhorias de Segurança](#melhorias-de-segurança)
5. [Fluxos de Trabalho](#fluxos-de-trabalho)
   - [Ciclo de Build e Testes](#ciclo-de-build-e-testes)
   - [Processo de Patch](#processo-de-patch)
   - [Gerenciamento de Versões](#gerenciamento-de-versões)

## Estrutura da Source

A source do Grand Chase Season V EP2 está organizada em vários diretórios principais, cada um com um propósito específico. Esta seção detalha a estrutura completa do código fonte e como os diferentes componentes se relacionam.

### Visão Geral dos Diretórios Principais

```
/
├── Client/                 # Código fonte do cliente do jogo
├── Client_Out/             # Arquivos de saída da compilação do cliente
├── Server/                 # Código fonte dos diferentes servidores
├── CommonFiles/            # Arquivos compartilhados entre cliente e servidor
├── Libs/                   # Bibliotecas de terceiros
├── Asset Converter/        # Ferramentas para manipulação de assets
└── Asset_De-Converter/     # Ferramentas para extrair assets
```

## Arquivos Principais

### Estrutura do Cliente

O diretório `/Client` contém o código principal do cliente do jogo. Abaixo estão os subdiretórios e arquivos mais importantes:

#### Arquivos Fundamentais

- **MyGame.vcxproj**: Projeto principal do Visual Studio para o cliente do jogo.
- **Procedure.cpp**: Contém o loop principal do jogo e o gerenciamento de estados (menus, gameplay, etc.).
- **Player.cpp/h**: Implementa a classe base para personagens jogáveis.
- **GCGlobal.cpp/h**: Definições globais e estruturas de dados fundamentais.
- **Monster.cpp/h**: Implementa a classe base para inimigos no jogo.
- **GCItemManager.cpp/h**: Gerencia todos os aspectos relacionados a itens (inventário, equipamentos, etc.).

#### Subdiretórios do Cliente

- **/GCUI/**: Contém os arquivos relacionados à interface do usuário.
  - **KGCState.cpp/h**: Classe base para os estados de jogo.
  - **KGCUIManager.cpp/h**: Gerencia os elementos da UI.
  - **KGCUIButton.cpp/h**: Implementação de botões de interface.
  - **KGCRoomScene.cpp/h**: Interface para salas de espera.
  - **KGCCharSelect.cpp/h**: Tela de seleção de personagens.
  
- **/Animation/**: Sistema de animação de personagens e objetos.
  - **GCAnimations.cpp/h**: Gerencia animações de objetos.
  - **KGCAnimManager.cpp/h**: Controla carregamento e reprodução de animações.
  - **KGCAnimEvent.cpp/h**: Sistema de eventos disparados durante animações.
  
- **/Particle/**: Sistema de partículas para efeitos visuais.
  - **GCParticleManager.cpp/h**: Gerencia todas as instâncias de partículas.
  - **GCParticleEvent.cpp/h**: Define eventos relacionados a partículas.
  - **GCParticleTemplate.cpp/h**: Templates para diferentes tipos de partículas.
  
- **/BuffSystem/**: Sistema de buffs e debuffs.
  - **GCBuff.cpp/h**: Implementação base para buffs e debuffs.
  - **GCBuffManager.cpp/h**: Gerencia buffs ativos em personagens.
  - **GCBuffEffect.cpp/h**: Efeitos visuais associados a buffs.
  
- **/HardDamage/**: Sistema de cálculo e aplicação de dano.
  - **DamageManager.cpp/h**: Gerencia a aplicação de dano.
  - **DamageInstance.cpp/h**: Representa uma instância específica de dano.
  - **DamageDefine.h**: Define constantes e tipos de dano.
  
- **/HardAI/**: Sistema de inteligência artificial.
  - **GCAIManager.cpp/h**: Gerencia comportamentos de IA.
  - **GCAIState.cpp/h**: Estados possíveis para entidades controladas por IA.
  - **GCAIAction.cpp/h**: Ações que podem ser executadas por entidades de IA.
  
- **/Kom/**: Componentes comuns do engine.
  - **KomThread.cpp/h**: Sistema de threading.
  - **KomFile.cpp/h**: Gerenciamento de arquivos.
  - **KomMemory.cpp/h**: Gerenciamento de memória.
  - **KomMath.cpp/h**: Funções matemáticas úteis para gráficos e física.
  
- **/GCUtil/**: Utilitários gerais.
  - **GCStringUtil.cpp/h**: Manipulação de strings.
  - **GCTimeUtil.cpp/h**: Funções relacionadas a tempo e temporização.
  - **GCRandom.cpp/h**: Geração de números aleatórios.
  
- **/GCDeviceLib/**: Interface com hardware.
  - **GCDeviceManager.cpp/h**: Gerencia acesso a dispositivos de input e output.
  - **GCDeviceTexture.cpp/h**: Gerencia texturas e recursos gráficos.
  - **GCDeviceSound.cpp/h**: Interface com sistema de áudio.
  
- **/Drama/**: Sistema de cutscenes e eventos cinemáticos.
  - **GCDramaManager.cpp/h**: Gerencia sequências cinemáticas.
  - **GCDramaEvent.cpp/h**: Eventos específicos de cutscenes.
  - **GCDramaAction.cpp/h**: Ações possíveis durante cutscenes.

#### Arquivos de Renderização

- **MyD3D.cpp/h**: Core do sistema de renderização DirectX.
- **MyD3D_Ex2.cpp/h**: Extensões do sistema de renderização.
- **GCGraphicsHelper.cpp/h**: Funções auxiliares para operações gráficas.
- **GCMeshObject.cpp/h**: Representação de modelos 3D no jogo.
- **GCSkeletalMeshObject.cpp/h**: Modelos 3D com animações esqueléticas.

#### Arquivos de Rede

- **Packet.cpp/h**: Definição e manipulação de pacotes de rede.
- **Operate Server.cpp/h**: Interface para comunicação com servidores.
- **KncNet.cpp/h**: Implementação de baixo nível para comunicação em rede.
- **LoginProcess.cpp/h**: Gerencia o processo de login.

### Estrutura do Servidor

O diretório `/Server` contém o código de todos os servidores que compõem o backend do jogo:

#### GameServer

- **GameServer.cpp/h**: Implementação principal do servidor de jogo.
- **GameServer_ClientHandler.cpp/h**: Gerencia conexões de clientes.
- **GameServer_ObjectManager.cpp/h**: Gerencia objetos e entidades no servidor.
- **GameServer_DungeonManager.cpp/h**: Controla instâncias de dungeons.
- **GameServer_PlayerHandler.cpp/h**: Processa ações de jogador.
- **Battle.cpp/h**: Lógica de combate no servidor.

#### CenterServer

- **CenterServer.cpp/h**: Implementação do servidor central.
- **ServerRegistry.cpp/h**: Registro de servidores disponíveis.
- **GlobalStateManager.cpp/h**: Gerencia estado global do jogo.
- **InterServerCommunication.cpp/h**: Comunicação entre servidores.

#### AgentServer

- **AgentServer.cpp/h**: Servidor de autenticação e roteamento inicial.
- **UserManager.cpp/h**: Gerencia informações de usuários conectados.
- **AuthenticationHandler.cpp/h**: Processa autenticação de usuários.
- **ServerSelector.cpp/h**: Seleciona servidor apropriado para o cliente.

#### MsgServer

- **MsgServer.cpp/h**: Implementação do servidor de mensagens.
- **ChatManager.cpp/h**: Gerencia sistema de chat.
- **FriendSystem.cpp/h**: Sistema de amigos.
- **GuildManager.cpp/h**: Sistema de guildas.
- **MailSystem.cpp/h**: Sistema de correio interno.

#### Arquivos Comuns do Servidor

- **BaseServer.cpp/h**: Classe base para todos os servidores.
- **DBLayer.cpp/h**: Interface com banco de dados.
- **NetLayer.cpp/h**: Camada de rede comum a todos os servidores.
- **SimLayer.cpp/h**: Camada de simulação para servidores de jogo.
- **ActorManager.cpp/h**: Gerencia entidades ativas no mundo do jogo.
- **LogManager.cpp/h**: Sistema de logging para depuração e monitoramento.
- **TickManager.cpp/h**: Gerencia o loop principal baseado em ticks.

### Bibliotecas e Dependências

O diretório `/Libs` contém bibliotecas de terceiros utilizadas pelo jogo:

- **/boost/**: Framework C++ para desenvolvimento multiplataforma.
- **/libxml/**: Biblioteca para processamento XML.
- **/curl/**: Biblioteca para transferências via protocolos de rede.
- **/lua/**: Linguagem de script utilizada pelo jogo.
- **/zlib/**: Biblioteca de compressão.
- **/sqldriver/**: Drivers para diferentes bancos de dados.
- **/PhysX/**: Biblioteca para simulação física.
- **/fmod/**: Biblioteca para processamento de áudio.

## Guias de Implementação

### Implementando Novos Personagens

Para adicionar um novo personagem ao Grand Chase, siga os passos abaixo:

1. **Definição do Personagem**:
   - Crie um arquivo de definição em `Client/CharacterData/{Nome}/CharDef.lua`.
   - Defina estatísticas base, animações, e habilidades.

2. **Modelo e Animações**:
   - Crie o modelo 3D no formato compatível (.X ou .mesh).
   - Prepare animações para cada estado (idle, run, jump, attack, skills, etc.).
   - Coloque os arquivos em `Client/Assets/Character/{Nome}/`.

3. **Implementação de Habilidades**:
   - Adicione definições de habilidades em `Client/SkillData/{Nome}/Skills.lua`.
   - Implemente efeitos visuais para habilidades em `Client/Particle/Templates/{Nome}/`.
   - Para habilidades especiais, modifique `GCSkill.cpp` para adicionar casos específicos.

4. **Interface e Ícones**:
   - Crie ícones para o personagem na seleção de personagens.
   - Adicione UI específica para habilidades do personagem.
   - Atualize `KGCCharSelect.cpp` para incluir o novo personagem.

5. **Registro no Servidor**:
   - Atualize `Server/GameServer/CharacterManager.cpp` para reconhecer o novo personagem.
   - Adicione entradas em `Server/Common/KCharacterDef.h` para o personagem.
   - Configure balanceamento inicial em `Server/GameServer/Balance.lua`.

6. **Testes**:
   - Teste todas as animações e transições.
   - Verifique colisões e hitboxes.
   - Balance habilidades e estatísticas conforme necessário.

### Adicionando Novas Armas e Itens

1. **Definição do Item**:
   - Adicione o item em `Client/ItemData/Items.lua`.
   - Defina categoria, atributos, preço, requisitos, etc.

2. **Modelo 3D (se aplicável)**:
   - Crie o modelo 3D para a arma/item.
   - Gere animações específicas se necessário.
   - Coloque em `Client/Assets/Items/{Categoria}/`.

3. **Icones e UI**:
   - Crie ícones para o item no inventário e loja.
   - Atualize descrições em `Client/StringTable/Items.lua`.

4. **Funcionalidade**:
   - Para itens consumíveis, implemente funcionalidade em `GCItemManager.cpp`.
   - Para armas, defina efeitos/partículas em `DamageManager.cpp`.
   - Para itens especiais, adicione casos específicos em `Player.cpp`.

5. **Database**:
   - Adicione o item às tabelas de banco de dados apropriadas.
   - Configure taxas de drop em `Server/GameServer/DropTable.lua`.

6. **Servidor**:
   - Atualize `Server/GameServer/ItemManager.cpp` para reconhecer o novo item.
   - Implemente lógica específica no servidor se necessário.

### Criando Novos Dungeons e Mapas

1. **Design do Mapa**:
   - Utilize o editor de mapas em `Client/GC_MapTool/`.
   - Defina layout, plataformas, checkpoints, e spawners.
   - Configure iluminação e efeitos ambientais.

2. **Configuração de Inimigos**:
   - Defina quais inimigos aparecerão e suas posições.
   - Configure padrões de spawn em `MapSystem/SpawnTable.lua`.
   - Defina comportamentos de IA específicos para o mapa.

3. **Eventos e Triggers**:
   - Adicione eventos específicos do mapa (cutscenes, diálogos).
   - Configure triggers para spawns especiais ou mudanças no ambiente.
   - Defina condições de vitória/derrota.

4. **Integração ao Jogo**:
   - Adicione o mapa à lista de mapas em `Client/MapSystem/MapList.lua`.
   - Configure requisitos e recompensas em `Client/MapSystem/Rewards.lua`.
   - Atualize a UI para mostrar o novo dungeon.

5. **Servidor**:
   - Adicione o mapa ao sistema de servidores em `Server/GameServer/MapManager.cpp`.
   - Configure lógica específica do servidor para o mapa.
   - Defina balanceamento em `Server/GameServer/DungeonBalance.lua`.

### Implementando Novos Eventos

1. **Design do Evento**:
   - Defina mecânicas, duração, e recompensas do evento.
   - Crie documento de especificação detalhando todas as funcionalidades.

2. **Implementação Cliente**:
   - Adicione UI específica do evento em `Client/GCUI/Event/`.
   - Implemente mecânicas específicas em `Client/EventSystem/`.
   - Crie assets visuais (banners, ícones, efeitos) para o evento.

3. **Implementação Servidor**:
   - Adicione lógica do evento em `Server/GameServer/EventManager/`.
   - Configure temporizadores e condições de início/fim.
   - Implemente sistema de recompensas.

4. **Integração ao Jogo**:
   - Atualize o menu principal para mostrar o evento ativo.
   - Adicione notificações e alertas sobre o evento.
   - Configure condições de participação.

5. **Configuração**:
   - Defina datas de início/fim em `Server/GameServer/EventSchedule.lua`.
   - Configure itens e recompensas específicas do evento.
   - Prepare sistema para ativar/desativar evento remotamente.

### Adicionando Novos Efeitos Visuais

1. **Design do Efeito**:
   - Defina aparência, duração, e comportamento do efeito.
   - Determine onde e quando o efeito será utilizado.

2. **Implementação de Partículas**:
   - Crie template de partículas em `Client/Particle/Templates/`.
   - Configure parâmetros (cor, tamanho, velocidade, vida útil).
   - Defina texturas e materiais para partículas.

3. **Implementação de Shaders**:
   - Para efeitos complexos, crie shaders específicos em `Client/Shaders/`.
   - Configure parâmetros de shader para diferentes condições.

4. **Integração ao Jogo**:
   - Para efeitos de habilidade, atualize `GCSkill.cpp`.
   - Para efeitos ambientais, atualize `MyD3D.cpp`.
   - Para efeitos de item, atualize `GCItemManager.cpp`.

5. **Otimização**:
   - Verifique performance em diferentes configurações.
   - Implemente LOD (Level of Detail) para efeitos complexos.
   - Configure limites máximos de partículas para evitar sobrecarga.

## Correções e Otimizações

### Problemas Conhecidos

Esta seção lista os principais problemas identificados na source atual que precisam de correção:

1. **Vazamentos de Memória**:
   - Em `Player.cpp`: Diversos objetos não são liberados corretamente na função `ReleasePlayerResource()`.
   - Em `GCItemManager.cpp`: Vazamento em `LoadItemDataFile()` quando carrega texturas de item.
   - Em `MyD3D.cpp`: Recursos DirectX não são liberados adequadamente em algumas situações.

2. **Bugs de Sincronização**:
   - Em `NetLayer.cpp`: Pacotes podem ser processados fora de ordem causando dessincronização.
   - Em `TickManager.cpp`: Eventos podem ser processados no tick errado devido a atrasos de rede.
   - Em `Player.cpp`: Estado de metamorfose pode dessincronizar entre cliente e servidor.

3. **Problemas de UI**:
   - Em `KGCUIManager.cpp`: Elementos de UI podem sobrepor incorretamente em certas resoluções.
   - Em `KGCChatting.cpp`: Mensagens longas podem causar problemas de renderização.
   - Em `KGCInventory.cpp`: Drag-and-drop de itens pode falhar em certas condições.

4. **Crashes Conhecidos**:
   - Em `Monster.cpp`: Acesso a ponteiro nulo quando um monstro é destruído durante animação.
   - Em `Procedure.cpp`: Crash durante transição entre estados específicos do jogo.
   - Em `DamageManager.cpp`: Acesso inválido à memória durante cálculos de dano complexos.

### Bugs Críticos

Estes são os bugs mais críticos que devem ser priorizados para correção:

1. **Exploit de Duplicação de Item**:
   - Em `GCItemManager.cpp`: Condição de corrida na função `EquipInventoryItem()` permite duplicar itens.
   - Correção: Implementar travamento adequado e verificação de integridade no servidor.

2. **Vulnerabilidade de Injeção SQL**:
   - Em `DBLayer.cpp`: Queries SQL são construídas sem sanitização adequada.
   - Correção: Implementar prepared statements e sanitização de inputs.

3. **Crash em Dungeons Específicas**:
   - Em `MapSystem.cpp`: Índice de array fora dos limites em mapas com muitos objetos.
   - Correção: Implementar verificação de limites e redimensionamento dinâmico de arrays.

4. **Dessincronização em PvP**:
   - Em `Battle.cpp`: Lógica de resolução de colisão pode divergir entre clientes.
   - Correção: Implementar autoritatividade do servidor para decisões finais.

5. **Memory Corruption em Loadings**:
   - Em `MyD3D.cpp`: Corrupção de memória durante carregamento de texturas grandes.
   - Correção: Implementar verificação de limites e gerenciamento de memória adequado.

### Otimizações Recomendadas

1. **Renderização**:
   - Implementar instancing para objetos repetitivos (`MyD3D.cpp`).
   - Melhorar culling para reduzir overdraw (`GCGraphicsHelper.cpp`).
   - Otimizar shaders para melhor performance em hardware mais antigo.

2. **Memória**:
   - Implementar object pooling para entidades frequentemente criadas/destruídas (`Player.cpp`, `Monster.cpp`).
   - Reduzir duplicação de texturas compartilhadas (`GCDeviceTexture.cpp`).
   - Implementar streaming de recursos mais eficiente (`GCDeviceManager.cpp`).

3. **Rede**:
   - Otimizar compressão de pacotes para reduzir largura de banda (`Packet.cpp`).
   - Implementar priorização de pacotes baseada em importância e visibilidade (`NetLayer.cpp`).
   - Melhorar handshake inicial para reduzir latência de conexão (`AgentServer.cpp`).

4. **Lógica de Jogo**:
   - Otimizar algoritmos de pathfinding para IA (`HardAI/GCPathfinder.cpp`).
   - Melhorar detecção de colisão para reduzir verificações desnecessárias (`DamageManager.cpp`).
   - Implementar multithreading para processos intensivos (`ThreadManager.cpp`).

### Melhorias de Segurança

1. **Autenticação**:
   - Substituir hash MD5 por algoritmos mais seguros (bcrypt, Argon2) em `AuthenticationHandler.cpp`.
   - Implementar autenticação de dois fatores.
   - Melhorar validação de sessão para prevenir hijacking.

2. **Comunicação Segura**:
   - Implementar criptografia TLS para todas as comunicações cliente-servidor.
   - Melhorar a implementação TEA em `Tea.cpp` ou substituir por algoritmo mais robusto.
   - Adicionar assinatura digital para pacotes críticos.

3. **Anti-Cheat**:
   - Implementar verificações de integridade de memória no cliente.
   - Adicionar validações serverside para todas as ações críticas.
   - Implementar sistema de report automático para comportamentos anômalos.

4. **Proteção de Dados**:
   - Implementar criptografia para dados sensíveis no banco de dados.
   - Melhorar anonimização de dados para compliance com regulações.
   - Implementar sistema de auditoria para operações críticas.

## Fluxos de Trabalho

### Ciclo de Build e Testes

1. **Preparação do Ambiente**:
   - Instale Visual Studio 2015+ com C++ e suporte MFC.
   - Instale DirectX SDK (June 2010).
   - Configure as variáveis de ambiente necessárias:
     - `DXSDK_DIR`: Aponta para o diretório do DirectX SDK.
     - `BOOST_DIR`: Aponta para o diretório do Boost.

2. **Compilação do Cliente**:
   - Abra `Season V EP2 Client.sln` no Visual Studio.
   - Selecione a configuração (Debug/Release).
   - Compile o projeto `MyGame`.
   - Os arquivos de saída serão gerados em `Client_Out/Debug/` ou `Client_Out/Release/`.

3. **Compilação do Servidor**:
   - Abra `Season V EP2 Server.sln` no Visual Studio.
   - Compile cada projeto de servidor individualmente na ordem:
     1. Common
     2. CenterServer
     3. AgentServer
     4. GameServer
     5. MsgServer
     6. Outros servidores

4. **Testes Locais**:
   - Configure um ambiente de teste local usando `Server/Config/Local.ini`.
   - Inicie os servidores na ordem:
     1. CenterServer
     2. AgentServer
     3. GameServer
     4. MsgServer
   - Execute o cliente com parâmetros de teste: `MyGame.exe -testmode -serverip=127.0.0.1`.

5. **Testes Automatizados**:
   - Execute testes unitários em `UnitTest/RunTests.bat`.
   - Verifique resultados em `UnitTest/Results/`.
   - Para testes de integração, use `IntegrationTests/RunTests.bat`.

### Processo de Patch

1. **Preparação**:
   - Identifique arquivos modificados desde a última versão.
   - Gere checksums para verificação de integridade.
   - Prepare notas de patch detalhando mudanças.

2. **Empacotamento**:
   - Use `Asset Converter/PatchBuilder.exe` para gerar pacote de patch.
   - Configure compressão e segmentação apropriadas.
   - Gere manifesto de arquivos para o cliente verificar.

3. **Distribuição**:
   - Faça upload do patch para servidores de distribuição.
   - Atualize configuração do servidor para reconhecer nova versão.
   - Prepare servidor de fallback caso ocorram problemas.

4. **Verificação**:
   - Teste o processo de patch em ambiente controlado.
   - Verifique integridade dos arquivos pós-patch.
   - Confirme que todas as funcionalidades continuam operacionais.

### Gerenciamento de Versões

1. **Nomenclatura**:
   - Format: `Season V EP2.X.Y.Z`
     - X: Major version (mudanças significativas)
     - Y: Minor version (novas funcionalidades)
     - Z: Patch version (correções)

2. **Controle de Mudanças**:
   - Mantenha um registro detalhado em `CHANGELOG.md`.
   - Documente todas as mudanças, incluindo:
     - Novas funcionalidades
     - Correções de bugs
     - Melhorias de performance
     - Mudanças de balanceamento

3. **Branching Strategy**:
   - `master`: Versão estável atual
   - `develop`: Próxima versão em desenvolvimento
   - `feature/x`: Funcionalidades específicas
   - `hotfix/x`: Correções urgentes

4. **Rollback Plan**:
   - Mantenha backups completos antes de cada atualização.
   - Prepare scripts para reverter mudanças em caso de problemas.
   - Documente procedimentos específicos para cada tipo de rollback. 
