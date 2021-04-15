# Introdução

Esse curso é sobre como **criar** e fazer **acompanhemento de progresso** utilizando SCORM (Sharable Content Object Reference Model) que nada mais é que uma coleção de padrões e especificações para e-learning baseado na web. Vamos aprender a pegar qualquer pedaço de HTML e embarcá-lo em um wrapper SCORM que vai permitir fazer o upload desse arquivo para qualquer LMS e ele ser capaz de ler os dados de progresso e atividades salvos.

Para fazer isso estaremos usando o [Rustici Driver](https://rusticisoftware.com/products/rustici-driver/) que pode ser aplicado em qualquer conteúdo HTML, Cascade Style Sheets (CSS) ou JavaScript (JS). Para que essa técnica funcione é necessário trabalhar com JS, então caso a pessoa que está tentando aprender esse conteúdo não tem proficiência com front-end é necessário que aprenda esses conceitos primeiramente.

## O que é um Learning Management System (LMS)?

Antes de aprender o que é SCORM e como ele funciona é necessário entender o que é um LMS e como ele funciona. Learning Management System ou LMS é um padrão da indústria de software para a administração, documentação, acompanhamento e back office de plataformas de apredizagem virtual.

Quando um curso é publicado em um LMS é possível ter a informação do andamento e desenvolvimento do aluno por parte da administração e dos professores do curso. O LMS em si tem a tarefa de administrar as tarefas, informações do aluno e do curso, os requisitos necessários entre cursos, trilhas de aprendizagem... é como um lugar para colocar diversos cursos e ter um repositório onde as pessoas podem encontrar esses cursos e também ao mesmo tempo uma base de dados que possui todas essas informações que o LMS controla e armazena sobre os conteúdos que os estudantes consomem na plataforma.

## O que é Sharable Content Object Reference Model (SCORM)?

Como vimos na Introdução SCORM é uma coleção de padrões da indústria. Esses padrões surgiram em 1999 e existem muitas versões compatíveis e incompatíveis entre si desse padrão que surgiram desde então, sendo a mais recentemente substituido pelos padrões xAPI e Tin Can API que possuem retrocompatibilidade com o mesmo. Porém, o modelo mais utilizado e popular do padrão ainda são as primeiras especificações do padrão SCORM, como o SCORM 2004.

O SCORM comunica-se com o LMS, então se você tem uma ferramenta de auditoria como Adobe Captivate ela vai ser capaz de ler informações do arquivo SCORM. Isso basicamente resume o que o SCORM realmente é, é uma forma de a ferramenta de auditoria e o LMS poderem se comunicar, tornando o curso um cliente a parte/separado de seu LMS ou sistema de administração.

Para que essa separação ser possível é necessário não apenas que os arquivos possam ser lidos, mas que também sejam preparados para que possam receber as informações no padrão SCORM. Se a pessoa está preparando o curso no Adobe Captivate ela é capaz de exportar isso em HTML 5 e o HTML 5 exportado pela ferramenta vem atrelado a um wrapper de SCORM que contêm um driver que é responsável por fazer a comunicação entre o arquivo e o LMS. Então quando o usuário iniciar o curso a partir desse arquivo com o driver do SCORM, o arquivo novamente começára a ser atualizado com a nova informação e por isso é importante que eles esteja pronto para tal.

O padrão SCORM é limitado nos tipos de conteúdo que ele consegue "acompanhar" (track), o que é um dos motivos que foi necessário uma nova especificação como a xAPI que permite acompanhar muito mais formas de conteúdo e de também fornecer mais informações sobre o curso a plataforma, mas é importante que o usuário conheça o padrão SCORM primeiramente porque ele é a fundação de como esses padrões funcionam, além de atualmente ser o padrão mais popular e suportado por ferramentas e outros LMS.

## Estrutura de um arquivo SCORM

Quando um projeto feito em uma ferramenta de auditoria como Adobe Captivate é publicada o arquivo SCORM em si nada mais é do que um .zip que contêm um grande conjunto de arquivos. Esses arquivos são divididos em dois grandes grupos:

 - **XML**: que são os arquivos que definem as informações básicas sobre o curso:
    - a versão do curso
    - qual arquivo inicia o curso
    - os requisitos para que esse curso possa ser cursado
    - metadados
    - quais tipos e quais arquivos compõe o curso...
- **JS**: Que são responsáveis pela lógica contida no arquivo, principalmente a comunicação por API com o LMS ou ferramente que está lendo o arquivo.

## O que o SCORM consegue monitorar?

Os principais elementos dos cursos que o SCORM é capaz de comunicar são:

- Se o curso foi completado
- Progresso (o aluno é capaz de retomar de onde parou)
- Notas
- (Session Data) Dados não padronizados, salvos pelo usuário
- (Interaction Data) Ações do usuário (onde ele clicou, o que marcou...)
- Quais páginas e conteúdos foram assistidos
- Pré-requisitos e continuações

A grande vantagem que o SCORM oferece é justamente a possibilidade de um curso poder ser importado/exportado para qualquer LMS permitindo que essa troca ocorra sem prejuízos para o aluno ou a administração do curso.

Por isso quaisquer "personalização" ou alteração no arquivo SCORM é profundamente desencorajada, uma vez que qualquer alteração fora do padrão mesmo que simples pode comprometer a habilidade de outros LMS conseguirem ler o arquivo.
