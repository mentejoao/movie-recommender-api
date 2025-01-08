# movie-recommender-api
 API de Recomendação de Filmes para a matéria de Domínios de Software (UFG) - 2024/02
# Assista AI
A ideia é que esta API de recomendação seja consumida pelo back-end e retorne uma quantidade top_k de id's, de uma fração selecionada, de filmes do [TMDB](https://www.themoviedb.org/?language=pt-BR).

A API possui dois principais casos de uso:
1. Recomendação Baseada no Usuário 
2. Recomendação Baseada em Conteúdo
   
##### Recomendação Baseada no Usuário 
* O modelo de recomendação baseada no usuário foi inspirado no modelo do curso de Machine Learning, do prof. Andrew Ng. Ele recomenda a partir da média de avaliação por gênero do usuário, portanto a ideia é que conforme o usuário avalie os filmes, tenhamos armazenados em um banco de dados estas avaliações (ou a média delas), de modo que para cada usuário logado no nosso site, tenhamos diferentes recomendações personalizadas baseadas em sua média por gênero. Consiste em uma rede neural que recebe dois vetores como entrada: o primeiro vetor é fixo e possui dimensões pre-estabelecidas, de acordo com a quantidade de gêneros e filmes disponíveis na nosso catálogo de filmes (provenientes do TMDB), este vetor possui os gêneros encodificados com one-hot encoding, portanto cada coluna representa um gênero; o segundo vetor representa a média de avaliação por gênero do usuário e é obtida no corpo da request, que o back-end fará pra nossa API, mais abaixo

##### Recomendação Baseada em Conteúdo 
* O modelo de recomendação baseada em conteúdo na realidade 
# Endpoints
## Obter recomendações baseada nas preferências do usuário
#### Método: ```GET```
#### URL: ```http://localhost/recommendations/user```
#### Body
```json
{
  "new_user_id": 12345,
  "new_rating_ave": 4.2,
  "new_action": 0,
  "new_adventure": 0,
  "new_animation": 3,
  "new_childrens": 0,
  "new_comedy": 3,
  "new_crime": 2.5,
  "new_documentary": 4,
  "new_drama": 5,
  "new_fantasy": 0,
  "new_horror": 5,
  "new_mystery": 5,
  "new_romance": 1,
  "new_scifi": 4,
  "new_thriller": 2.5,
  "new_rating_count": 120,
  "top_k": 10
}
```

## Obter recomendações baseada em conteúdo
#### Método: ```GET```
#### URL: ```http://localhost/recommendations/content```
#### Body
```json
{
  "search": "Fifty Shades of Grey",
  "top_k": 10
}
```
## Diagrama de Sequência
##### Segundo caso de uso
![image](https://github.com/user-attachments/assets/408a19de-8f43-405d-a6f1-59e1dd52be28)
