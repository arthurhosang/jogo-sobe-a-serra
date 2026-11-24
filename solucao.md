function pilotoAutomatico(controle, sensor) {

  // Espaço livre (em metros) em cada faixa
  const espacoEsquerda = sensor.distanciaObstaculo(ESQUERDA);
  const espacoMeio     = sensor.distanciaObstaculo(MEIO);
  const espacoDireita  = sensor.distanciaObstaculo(DIREITA);
  const espaco = [espacoEsquerda, espacoMeio, espacoDireita];

  // Qual faixa tem MAIS espaço?
  let melhor = sensor.faixa;
  if (espacoEsquerda > espaco[melhor]) melhor = ESQUERDA;
  if (espacoMeio     > espaco[melhor]) melhor = MEIO;
  if (espacoDireita  > espaco[melhor]) melhor = DIREITA;

  // Obstáculo perto? Vai pra melhor faixa
  if (espaco[sensor.faixa] < 25) {
    if (melhor < sensor.faixa) {
      controle.paraEsquerda();
    }
    if (melhor > sensor.faixa) {
      controle.paraDireita();
    }
  }
}