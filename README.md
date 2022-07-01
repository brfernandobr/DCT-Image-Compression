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

> Este projeto consiste em desenvolver um Jupyter Notebook em linguagem Python para executar a compressão *lossy* de imagens usando a Transformada Discreta de Cosseno (DCT, na sigla em inglês). Este algoritmo é amplamente usado por diversos padrões populares, como o JPEG para compressão de imagens e o MPEG para compressão de vídeos. O termo inglês *lossy* significa que a imagem obtida possui perda de qualidade em relação à imagem original, em oposição a uma compressão *lossless* em que não há perda de qualidade.
>
> A motivação vem da constatação de que, sem técnicas adequadas de compressão de imagens e vídeos como a efetuada pelo algoritmo DCT, a internet não existiria na forma como a conhecemos hoje. Serviços de hospedagem de fotografias e imagens, bem como a sua troca pela internet, seriam bastante impactados caso tivessem que usar arquivos *bitmap* sem compressão ou *png* com compressão *lossless*. Aplicações *web* como o YouTube, para hospedagem de vídeo, dificilmente poderiam existir, bem como serviços de vídeoconferência e vídeoaulas *online*. Podemos dizer que o impacto do algoritmo DCT se estende a praticamente todas as áreas da vida cotidiana, como lazer, trabalho, educação etc.
>
> O objetivo principal é investigar a relação entre a taxa de compressão utilizada pelo algoritmo de compressão e o impacto na qualidade da imagem assim obtida.

## Abordagem Adotada

> Qualquer computador ou telefone celular atual possui algum software ou circuito eletrônico dedicado que realiza compressão DCT de forma extremamente eficiente. Portanto neste projeto buscamos adotar uma abordagem mais investigativa e educativa, do que propriamente obter um arquivo JPEG ao final. Criamos um Jupyter Notebook em linguagem Python que realiza:
>
> - O algoritmo DCT de duas formas distintas: inicialmente, o DCT usando quatro *loops for* aninhados com 8196 cálculos de cosseno por bloco 8x8 de pixels monocromáticos; em seguida, implementamos o DCT de forma mais rápida e eficiente por meio de duplo produto matricial empregando uma matriz de transformação ortogonal T;
> - Todos os cálculos intermediários forma executados usando float64. Numa implementação prática do algoritmo seria usada uma precisão menor, para maior rapidez e menor uso de recursos de hardware;
> - Obtivemos as 64 funções-base, ou imagens-base, que formam a base do espaço vetorial do DCT no domínio da frequência;
> - Implementamos a etapa de quantização dos coeficientes DCT e investigamos a relação entre a qualidade (valor inteiro de 1 a 100) usada na quantização e o resultado obtido;
> - Implementamos uma função de RLE (Run-Length Encoding) que percorre a matriz 8x8 de coeficientes DCT quantizados em zigue-zague, iniciando no canto superior esquerdo, e calcula e exibe na tela o resultado do algoritmo;
> - Por fim, aplicamos o algoritmo de compressão DCT com quantização e RLE em algumas imagens de exemplo, cada qual com diversas intensidades de quantização de 1 a 100.
>
> Várias simplicações foram adotadas:
>
> - Não foi implementada a Codificação de Huffman após o RLE;
> - Não obtemos um arquivo JPEG ao final do processo;
> - Não foi implementado Chroma Subsampling, pois queríamos ver o resultado obtido apenas com a quantização;
> - Imagens com resolução não múltipla de 8x8 sofrem corte nos pixels excedentes à direita e em baixo;
> - O algoritmo não aceita imagens com canal alpha.

## Resultados Finais

> Os resultados encontram-se no arquivo DCT_Image_Compression.html (versão html do Jupyter Notebook após executar todas as suas células de código), disponível para *download* neste link:
>
> https://drive.google.com/file/d/1VHdBVZEHQAfKBDNNeE1MuEYi6m1rfLfz/view?usp=sharing

## Conclusões

> Da execução do Jupyter Notebook conseguimos tirar algumas conclusões:
>
> - Ao aplicarmos DCT e logo em seguida IDCT (DCT Inverso) em um bloco 8x8 monocromático, usando float64 em todas as etapas de cálculo e armazenamento dos resultados, conseguimos obter de volta a matriz 8x8 de pixels original com erro da ordem de 10^-13 (erro que atribuímos a erros de arredondamento dos coessenos e da representação em ponto flutuante). Portanto consideramos que o DCT e o IDCT são absolutamente "lossless" (sem perdas);
> - Ao aplicarmos DCT e logo em seguida IDCT (DCT Inverso) em um bloco 8x8 monocromático com saltos de 0 a 255 (ou de -128 a +127) entre pixels vizinhos na mesma linha ou na mesma coluna, obtemos de volta a matriz de pixels original, novamente com erro da ordem de 10^-13. Portanto consideramos que o DCT consegue codificar qualquer salto entre dois pixels vizinhos;
> - Os coeficientes DCT estão na faixa de -1024 a +1023 em ponto flutuante. A mínima representação para eles é de inteiro de 11 bits com sinal, mas esta representação com inteiros incorre em erros de arredondamento;
> - Após aplicarmos DCT com quantização em algumas imagens, percebemos que o uso da qualidade padrão (de valor 50) na quantização representa um ótimo compromisso entre qualidade e compressão. Baixos valores de qualidade resultam em artefatos de compressão como blocos e lagoas de quantização bastante pronunciados, especialmente em áreas da imagem com sutil variação entre os pixels, como por exemplo em nuvens, céu, paredes, água etc. Um outro tipo de artefato de compressão gerado pela quantização chama-se Mosquito Noise: de forma semelhante a mosquitos voando em torno de uma pessoa, esse tipo de distorção da imagem aparece próxima a contornos nítidos de um objeto;
> - Ao tentarmos aplicar valores de qualidade de quantização muito altos, de 90 a 100, percebemos que o resultado às vezes tem tamanho em bytes até maior que a quantidade de bytes da imagem sem compressão, o que desvirtua totalmente o propósito da aplicação do algoritmo;
> - Consegue-se um melhor resultado baixando a resolução em pixels da imagem original e aplicando uma quantização com qualidade igual a 50 do que usando a imagem original e aplicando um valor baixo de qualidade. Qualidade igual a 50 deveria ser a qualidade mínima usada. Caso o tamanho em bytes da imagem final fique acima do desejado, é preferível baixar a resolução da imagem original do que baixar a qualidade da quantização.

## Referências Bibliográficas

> https://en.wikipedia.org/wiki/Discrete_cosine_transform
> 
> https://en.wikipedia.org/wiki/JPEG
> 
> https://www.math.cuhk.edu.hk/~lmlui/dct.pdf
