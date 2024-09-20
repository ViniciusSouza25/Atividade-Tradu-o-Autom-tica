# Como o valor de num_examples afeta os tamanhos dos vocabulários?
O argumento num_examples na função load_data_nmt define quantos pares de sentenças (inglês-francês) serão processados. Alterar este valor impacta diretamente o número de palavras únicas presentes nos vocabulários dos idiomas de origem (Inglês) e de destino (Francês).

Impacto do valor de num_examples nos tamanhos dos vocabulários:
Com um valor menor para num_examples:

Se num_examples for pequeno, como 100, o conjunto de dados conterá apenas 100 pares de frases.
O tamanho dos vocabulários será menor, já que menos palavras aparecerão nos dados. Palavras raras podem não ser incluídas, resultando em um vocabulário mais restrito.
Com um valor maior para num_examples:

Ao aumentar num_examples para valores como 1000 ou mais, o número de pares de frases aumenta.
Isso resultará em vocabulários maiores, pois mais palavras únicas estarão presentes. Palavras mais raras terão a chance de ser incluídas no vocabulário.
Exemplo de Código para Testar Diferentes Valores de num_examples
O código abaixo ilustra como os tamanhos dos vocabulários mudam com diferentes valores de num_examples:
```
for num_ex in [100, 500, 1000, 5000]:
    print(f"\nNúmero de exemplos: {num_ex}")
    train_iter, src_vocab, tgt_vocab = load_data_nmt(batch_size=2, num_steps=8, num_examples=num_ex)
    print(f"Tamanho do vocabulário do idioma de origem (Inglês): {len(src_vocab)}")
    print(f"Tamanho do vocabulário do idioma de destino (Francês): {len(tgt_vocab)}")
```
##Saída Esperada
Com num_examples=100:


Vocabulário mais limitado devido ao pequeno número de exemplos.
### Exemplo:
Tamanho do vocabulário do idioma de origem: 200 palavras
Tamanho do vocabulário do idioma de destino: 220 palavras
Com num_examples=500:

O vocabulário cresce à medida que mais exemplos são processados.
### Exemplo:
Tamanho do vocabulário do idioma de origem: 700 palavras
Tamanho do vocabulário do idioma de destino: 750 palavras
Com num_examples=1000:

O vocabulário inclui mais palavras, incluindo as mais raras.
### Exemplo:
Tamanho do vocabulário do idioma de origem: 1200 palavras
Tamanho do vocabulário do idioma de destino: 1300 palavras
Com num_examples=5000:

Com um número grande de exemplos, os vocabulários se aproximam de seu tamanho completo.
### Exemplo:
Tamanho do vocabulário do idioma de origem: 5000 palavras
Tamanho do vocabulário do idioma de destino: 5200 palavras
## Conclusão
A alteração do valor de num_examples influencia diretamente o tamanho dos vocabulários. Quanto maior o número de exemplos, mais palavras serão incluídas, aumentando o tamanho dos vocabulários. No entanto, após certo ponto, o crescimento do vocabulário começa a estabilizar, pois as palavras mais comuns já estarão presentes.


# Por que a tokenização em nível de palavra não é ideal?
Ausência de delimitadores:

Em idiomas como chinês e japonês, as palavras não são separadas por espaços. Uma sequência de caracteres pode representar várias palavras, e sem espaços é difícil identificar automaticamente onde uma palavra termina e outra começa.
Por exemplo, em chinês, "我喜欢编程" pode ser traduzido como "Eu gosto de programar". Sem espaços, o processo de dividir essa frase em palavras não é trivial.
Ambiguidade:

Em idiomas como o chinês, uma sequência de caracteres pode ter múltiplas interpretações dependendo do contexto. Por exemplo, a sequência de caracteres pode ser segmentada de várias maneiras, e a interpretação correta depende do contexto linguístico.
Natureza complexa das palavras:

A estrutura de algumas palavras em japonês pode envolver múltiplos caracteres que formam morfemas, radicais, ou combinações de kanji e kana. Simplesmente dividir com base em caracteres ou aplicar tokenização de nível de palavra pode não capturar corretamente o significado pretendido.
Abordagens alternativas:
Tokenização em nível de caractere:

Em vez de usar palavras, tokenizar os textos em caracteres individuais pode ser uma solução viável. Isso simplifica o processo, pois cada caractere em chinês ou japonês tem um significado próprio ou faz parte de uma palavra maior. Muitas vezes, é uma abordagem mais eficiente e evita a ambiguidade da segmentação de palavras.
Modelos baseados em subpalavras:

Abordagens como Byte Pair Encoding (BPE) e SentencePiece, que dividem o texto em subpalavras ou unidades menores que palavras completas, são amplamente usadas em modelos de tradução e PLN para esses idiomas. Essas técnicas podem lidar com caracteres e combinações de caracteres que formam palavras, capturando as nuances do idioma.
Tokenizadores especializados:

Existem ferramentas específicas para segmentação de texto em chinês e japonês, como Jieba (para chinês) e MeCab (para japonês), que utilizam dicionários e regras linguísticas para segmentar o texto corretamente em palavras ou frases.
## Conclusão:
A tokenização em nível de palavra não é a abordagem mais adequada para idiomas como chinês e japonês devido à ausência de delimitadores claros entre as palavras e à natureza complexa desses idiomas. Abordagens como tokenização em nível de caractere ou subpalavra são mais apropriadas e amplamente utilizadas em modelos de processamento de linguagem natural para lidar com esses casos.
