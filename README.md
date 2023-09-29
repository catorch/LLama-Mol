
---

# LLaMA MOL: Generating Molecules for Drug Discovery with LLaMA

![LLaMA - MOL](assets/llama-mol.png) 

## I. Problema

El diseño y descubrimiento de nuevos medicamentos es uno de los desafíos más importantes y complejos en la investigación biomédica, ya que esto permite la síntesis y caracterización de una vasta gama de moléculas que tienen el potencial de mejorar la salud humana. Sin embargo, se estima que el número de moléculas potencialmente sintetizables para uso farmacéutico se encuentra alrededor de 10^60, lo que plantea un desafío importante. Dentro de este contexto, la química medicinal se ha esforzado por descubrir y diseñar compuestos que no solo sean eficaces para tratar enfermedades, sino que también sean seguros para los pacientes. Pero abordar la totalidad del universo de moléculas posibles se vuelve impráctico desde un punto de vista económico y temporal. Ante este panorama, la necesidad de herramientas computacionales ha cobrado especial relevancia para afinar la búsqueda y enfocar los esfuerzos en candidatos prometedores.

En este contexto, dos estrategias computacionales han cobrado relevancia: el cribado virtual (“Virtual Screening” en inglés) y el diseño de fármacos “de novo”. Por un lado, el cribado virtual consiste en buscar en una vasta biblioteca de moléculas aquellas que cumplan con ciertos criterios. Para esto se utilizan métricas basadas en la similitud para determinar cuán semejante es una molécula a otra ya conocida por su actividad biológica. Por otro lado, el diseño de fármacos “de novo” no busca en moléculas existentes, sino que se trata de crear moléculas completamente nuevas que sean efectivas contra un objetivo biológico específico.

Históricamente, el diseño de fármacos de novo ha seguido dos estrategias principales. La primera se basa en ensamblar moléculas a partir de grupos atómicos o fragmentos predefinidos. Sin embargo, esta estrategia puede conducir a moléculas que resulten difíciles de sintetizar en un laboratorio. La segunda estrategia utiliza reacciones químicas simuladas virtualmente, basadas en reglas definidas por expertos, que pretenden reflejar métodos de síntesis en laboratorio. Aunque esta metodología produce moléculas más prácticas y similares a fármacos, no está exenta de limitaciones, como la posibilidad de no predecir con precisión todas las reacciones químicas.

Dada la complejidad del diseño de fármacos, el surgimiento del aprendizaje automático y las redes neuronales ha ofrecido una nueva perspectiva prometedora. Dentro de la amplia gama de arquitecturas de redes neuronales, el trabajo de Segler et al. demuestra que la utilización de Redes Neuronales Recurrentes (RNNs), comúnmente utilizada en áreas como el procesamiento de lenguaje natural, resulta efectivo para la generación de moléculas, ya que las estructuras químicas pueden representarse como secuencias (por ejemplo, utilizando la notación SMILES), y, por lo tanto, es plausible tratar la generación de moléculas como un problema de generación de secuencias, similar a problemas de procesamiento de lenguaje natural. Además, el enfoque de este trabajo demuestra otra ventaja significativa de esta técnica: puede ser afinado (fine-tuned). Si se tiene un conjunto de moléculas conocidas por ser efectivas contra un objetivo biológico específico, se puede afinar la RNN con este conjunto más pequeño, permitiendo que el modelo se especialice en generar moléculas activas contra ese objetivo específico.  De esta manera, la integración de RNNs en este proceso ofrece un enfoque más eficiente, preciso y coste-efectivo.

En el trabajo de Segler et al Se utilizó una arquitectura de RNN que consistía en tres capas LSTM (Long Short-Term Memory), cada una con 1024 dimensiones, sumando un total de 21.3x 10^6 parámetros. Las LSTM, una variante especializada de RNNs, son especialmente adecuadas para aprender dependencias a largo plazo y patrones en secuencias, lo que es esencial al considerar la complejidad y longitud de las notaciones moleculares como SMILES. Aunque este enfoque ha mostrado resultados prometedores, la evolución en el campo del aprendizaje profundo ha llevado al surgimiento de arquitecturas más avanzadas, como el modelo transformador.

El modelo transformador, y específicamente LLaMA (Large Language Model Meta AI), ha revolucionado el campo del procesamiento del lenguaje natural con su innovador mecanismo de atención, que permite al modelo centrarse en diferentes partes de una secuencia cuando genera una salida. Este mecanismo de atención le da al modelo la capacidad de capturar relaciones a largo plazo en los datos, similar a las LSTMs, pero con una mayor eficiencia y flexibilidad.

LLaMA, en particular, ha demostrado ser superior en tareas de procesamiento del lenguaje natural debido a su masiva cantidad de parámetros y su arquitectura optimizada. A diferencia de la RNN utilizada por Segler, que tenía 21.3x10^6 parámetros, LLaMA cuenta con modelos que varían desde 7 mil millones hasta 70 mil millones de parámetros, permitiendo una representación más compleja y una capacidad de aprendizaje más profunda.
Debido a estas ventajas, en el presente trabajo, se optó por utilizar LLaMA para el diseño de la generación de moléculas de novo. Aunque las RNNs, como las utilizadas por Segler, han demostrado ser efectivas, la hipótesis del presente trabajo es que la capacidad de LLaMA para manejar secuencias largas y su mecanismo de atención mejorado pueden ofrecer resultados aún más prometedores. Al entrenar y afinar LLaMA en conjuntos de datos de moléculas farmacéuticamente relevantes, se busca no solo acelerar el proceso de descubrimiento de medicamentos, sino también reducir el espacio de búsqueda de las moléculas potencialmente sintetizables y efectivas.

---
### Referencias
* Segler, M. H. S., Kogej, T., Tyrchan, C., & Waller, M. P. (2018). Generating Focused Molecule Libraries for Drug Discovery with Recurrent Neural Networks. *ACS Central Science, 4*(1), 120-131. https://doi.org/10.1021/acscentsci.7b00512