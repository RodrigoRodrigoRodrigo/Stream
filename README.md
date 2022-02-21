package application;

import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

public class Program {

	public static void main(String[] args) {

		List<Integer> list = Arrays.asList(3, 4, 5, 10, 7);
			
		Stream<Integer> st1 = list.stream();// a minha lista list.stream, isso é criar uma stream apartir da lista.
		System.out.println(Arrays.toString(st1.toArray()));
		/*
		 * agora pra testar, eu vou mandar imprimir essa stream na tela, pra imprimir a stream na tela, eu posso 
		 * chamar essa operação terminal, que é o toArray, o toArray ele converte a minha stream para um vetor.
		 */
		//--------------------------------------------------------------------------------------------------------------
		
		Stream<String> st2 = Stream.of("Maria", "Alex", "Bob");
		/*
		 * o metodo stream.of, esse metodo me permite colocar os elementos diretamente aqui entre parenteses.
		 */
		System.out.println(Arrays.toString(st2.toArray()));
		//--------------------------------------------------------------------------------------------------------------
		
		Stream<Integer> st3 = Stream.iterate(0, x -> x + 2);
		/*
		 * esse iterate aqui, eu vou falar o seguinte, quem é o primeiro elemento da minha stream? eu vou falar que é 0
		 * e qual é a função de iteração de geração dos proximos elementos? eu vou falar assim ó, é x que leva(->) a x
		 * + 2. perceba que essa stream ela é potencialmente infinita, eu vou somando aqui + 2 + 2 + 2.. indefinidamente
		 * então agora, como que eu vou consumir essa stream e processar alguns elementos? eu vou chamar aquela função
		 * short-circuit que é a limit. 
		 */
		System.out.println(Arrays.toString(st3.limit(10).toArray()));
		/*
		 * eu vou mandar imprimir aqui o Arrays.toString(), agora eu vou fazer assim ó, (st3 que é a minha stream
		 * .limit(), ai eu vou falar assim, eu quero um .limit(10) de 10 elementos. Essa operação ela é uma operação
		 * intermediaria, ela vai me devolver uma nova stream e ai essa nova stream eu vou chamar o .toArray() apartir
		 * dela, pra transformar pra vetor pra pode imprimir aqui ó(Arrays.toString).
		 */
		
		//--------------------------------------------------------------------------------------------------------------
		 //isso é uma sequencia de de fibonacci
		Stream<Long> st4 = Stream.iterate(new long[] { 0L, 1L }, p -> new long[] { p[1], p[0] + p[1] }).map(p -> p[0]);
		/*
		 * apartir do  Stream.iterate, só que aqui eu vou ter que fazer um macete, o java ele não tem a dupla, o parcinho
		 * de numeros, eu vou fazer o seguinte, eu vou dizer assim, vou dizer que o primeiro elemento dessa stream 
		 * vai ser um new Long[], um array com os elementos {0L(long), e 1L(long)}, ok esse vai ser o primeiro elemento
		 * aqui da minha stream, em seguida a função de geração dessa stream vai ser oque? vai ser um objeto p que leva
		 * (->) num novo array de long, new long[] contendo tambem dois elementos, o primeiro elemento desse array
		 * vai ser o array anterior na posição 1{p[1], e o segundo elemento aqui desse array vai ser o elemento anterior
		 * na posição 0 p[0] + o elemento anterior na posição 1 p[1]}, que é a soma dos dois interiores.
		 * isso aqui vai gerar pra mim uma stream de pares, mas eu não quero uma stream de pares, eu quero uma stream de
		 * long(Stream<Long> st4), então agora eu vou lançar aqui a função map pra transformar esses pares em apenas um
		 * elementos, então eu vou fazer assim ó, .map(pra cada par do elemento p, eu simplesmente vou pegar o p na
		 * posição 0 p[0].
		 */
		System.out.println(Arrays.toString(st4.limit(10).toArray()));
		/*
		 * eu vou mandar imprimir aqui o Arrays.toString(), agora eu vou fazer assim ó, (st3 que é a minha stream
		 * .limit(), ai eu vou falar assim, eu quero um .limit(10) de 10 elementos. Essa operação ela é uma operação
		 * intermediaria, ela vai me devolver uma nova stream e ai essa nova stream eu vou chamar o .toArray() apartir
		 * dela, pra transformar pra vetor pra pode imprimir aqui ó(Arrays.toString).
		 */

	}

}
