# Algoritmo de compressão de imagens baseado em DCT
# DCT-based image compression algorithm

## Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de pós-graduação *EA979A - Introdução a Computação Gráfica e Processamento de Imagens*, oferecida no primeiro semestre de 2022, na Unicamp, sob supervisão da Profa. Dra. Paula Dornhofer Paro Costa, do Departamento de Engenharia de Computação e Automação (DCA) da Faculdade de Engenharia Elétrica e de Computação (FEEC).

> Integrantes do grupo:
> 
> |Nome  | RA | Curso|
> |--|--|--|
> | Fernando Brasil Sales  | 265268  | Eng. de Computação |


## Descrição do Projeto
> Este projeto consiste em desenvolver um programa em linguagem Python para executar a compressão *lossy* de imagens usando a Transformada Discreta de Cosseno (DCT, na sigla em inglês). Este algoritmo é amplamente usado por diversos padrões populares, como o JPEG para compressão de imagens e o MPEG para compressão de vídeos. O termo inglês *lossy* significa que a imagem obtida possui perda de qualidade em relação à imagem original, em oposição a uma compressão *lossless* em que não há perda de qualidade.
> 
> A motivação vem da constatação de que, sem técnicas adequadas de compressão de imagens e vídeos como a efetuada pelo algoritmo DCT, a internet não existiria na forma como a conhecemos hoje. Serviços de hospedagem de fotografias e imagens bem como a sua troca pela internet seriam bastante impactados caso tivessem que usar arquivos *bitmap* sem compressão ou *png* com compressão *lossless*. Aplicações *web* como o YouTube, para hospedagem de vídeo, dificilmente poderiam existir, bem como serviços de vídeoconferência e vídeoaulas *online*. Podemos dizer que o impacto do algoritmo DCT se estende a praticamente todas as áreas da vida cotidiana, como lazer, trabalho, educação etc.
> 
> O objetivo principal é investigar qual é a relação entre o nível ou taxa de compressão utilizada pelo algoritmo de compressão e o impacto na qualidade da imagem assim obtida.


## Plano de Trabalho
> * Etapa 1 (até o final de abril/2022): Estudo teórico do algoritmo DCT e do padrao JPEG
> 
>     Será necessários estudar, dentre outras coisas:
>     - Conversão do espaço de cores RGB para o espaço YCbCr
>     - Chroma subsampling, em particular com taxa 4:2:0
>     - Separação ou quebra da imagem em blocos 8x8, 16x8 ou 16x16
>     - O algoritmo DCT, que consiste na decomposição da imagem de cada bloco nas componentes de frequência espacial
>     - Quantização, que consiste em um truncamento para descartar altas frequências
>     - Codificação entrópica, que consiste em uma codificação *lossless*, para armazenar de forma eficiente os dados obtidos da quantização
>     
> 
> * Etapa 2 (mês de maio/2022): codificação do algoritmo em Python
> 
>     Consistirá em tentar implementar na linguagem Python o algoritmo estudado na etapa anterior.
>     
> * Etapa 3 (mês de junho/2022): testes, aprimoramentos e elaboração do relatório final


## Referências Bibliográficas
> https://en.wikipedia.org/wiki/Discrete_cosine_transform
> 
> https://en.wikipedia.org/wiki/JPEG
> 
> https://www.math.cuhk.edu.hk/~lmlui/dct.pdf
