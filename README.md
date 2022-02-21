package application;

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Program {

	public static void main(String[] args) {

		List<Integer> list = Arrays.asList(3, 4, 5, 10, 7);
		
		// a minha lista list.stream, isso é criar uma stream apartir da lista.
		Stream<Integer> st1 = list.stream().map(x -> x * 10);
		/*
		 * o map é uma operação intermediaria que transforma lista, ele vai pegar cada elemento x da minha lista
		 * e vai transformar em outro elemento(->) conforme eu definir aqui na minha expressão lambda, então por ex
		 * x -> x * 10, aqui eu estou gerando uma outra stream onde cada elemento dessa outra stream vai ser o elemento
		 * original vezes 10.
		 */
		System.out.println(Arrays.toString(st1.toArray()));
		/*
		 * o toArray é uma operação terminal, eu to aplicando uma operação intermediario(.map(x -> x * 10)), e depois
		 * eu aplico aqui a operação terminal aqui, ai ele vai processar a stream e vai me dar o resultado.
		 */
		
		//--------------------------------------------------------------------------------------------------------------
		
		int sum = list.stream().reduce(0, (x, y) -> x + y);
		/*
		 * eu vou somar todos os elementos da minha stream, como eu vou fazer isso? eu vou chamar o list.stream() pra
		 * criar uma stream apartir da minha lista, e ai eu chamar a operação reduce, o reduce ele pegar um elemento
		 * iniciar, que vai ser o elemento neutro da sua operação, e depois uma função que recebe dois argumentos
		 * e gera um resultado, no caso aqui vai ser a dunção de soma, então aqui vai ser x, y que são os argumentos.
		 * e resultando(->) na operação x + y.
		 */
		System.out.println("Sum = " + sum);
		
		//--------------------------------------------------------------------------------------------------------------
		
		//vou fazer um pipeline maior
		List<Integer> newList = list.stream()
				.filter(x -> x % 2 == 0)
				.map(x -> x * 10)
				.collect(Collectors.toList());
		/*
		 * eu vou criar uma nova lista de inteiros, vou chamar de newList e ai eu vou fazer o seguinte, vou fazer minha
		 * list.stream, pra gerar uma stream, e agora eu vou fazer algumas operações intermediarias, primira delas vai
		 * ser o .filter(), o filtee ele filtra minha lista, eu vou dar um predicado, e ai com base nesse predicado
		 * vai ser gerado uma nova stream pra mim contendo apenas os elementos que satisfazem aquele predicado
		 * então por ex: eu vou querer todo elemento x .filter(x tal que(->) x mod(%)2 == 0); ou seja, eu vou querer
		 * todos os elementos pares, beleza, filtrei a minha stream agora nessa stream resultante eu vou aplicar a
		 * operação .map, pra transformar em outra stream , eu vou pegar cada elemento da minha stream de numeros pares
		 * e transformar ele no x * 10 (.map(x -> x * 10) então eu estou gerando uma nova stream onde cada elemento vai
		 * ser o original multiplicado por 10, e agora eu vou aplicar aqui uma operação terminal pra transformar essa
		 * stream resultante numa lista, pra transformar uma stream em lista a gente vai chamar o .collect e entre ( ) 
		 * (collectores.toList());
		 */
		System.out.println(Arrays.toString(newList.toArray()));
		/*
		 * o que aconteceu com o resultado? o meu pipeline pegou a stream gerada por essa lista(linha12), filtrou 
		 * somente os numeros pares que era o 4 e o 10, e multiplicou cada um por 10, olha que bacana o pipeline.
		 */
	}

}
