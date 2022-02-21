package application;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Locale;
import java.util.Scanner;
import java.util.stream.Collectors;

import entities.Product;

public class Program {

	public static void main(String[] args) {

		Locale.setDefault(Locale.US);
		Scanner sc = new Scanner(System.in);
		
		System.out.print("Enter full file path: ");
		String path = sc.nextLine();
		// aqui eu peço pro usuario digitar o caminho do arquivo e leio na variavel path
		
		try (BufferedReader br = new BufferedReader(new FileReader(path))) {
			/*
			 * aqui eu vou fazer um bloco try with resources abrindo o arquivo, ai eu vou instanciar uma List de 
			 * produtos e vou ler o meu arquivo
			 */
			List<Product> list = new ArrayList<>();
			
			String line = br.readLine(); // vou ler uma linha
			while (line != null) { // e enquanto essa linha foi diferente de nullo
				String[] fields = line.split(","); 
				/*
				 * eu vou fazer um split nessa linha, por que o split? por que o split ele vai recortar esse 
				 * String em dois de forma que eu possa acessar o nome e preço, o resultado disso vai ficar nesse
				 * vetor chamado fields e ai eu vou instanciar o produto.
				 */
				list.add(new Product(fields[0], Double.parseDouble(fields[1])));
				/*
				 * fields na posição zero vai ser o nome, e o fields na posição um vai ser o preço, ai eu vou dar o
				 * Double.parseDouble para converter o numero para double..
				 * feito isso eu vou mandar ler a proxima linha e assim por diante ate acabar o arquivo.
				 */
				line = br.readLine();
			}
			
			double avg = list.stream()
					.map(p -> p.getPrice()) // essa é pra minha lista que é de produtos e eu quero só o preço. e agora eu gerei uma nova stream so com os preços dos produtos.
					.reduce(0.0, (x,y) -> x + y) / list.size();
					/*
					 * a reduce ela vai me permitir a fazer o somatorio dos preços.
					 * então eu vou começar com zero e vou dizer que a função aqui pra aplicar em cada elemento para par
					 * vai ser x,y levando a(->) x + y, com isso aqui eu achei a soma de todo mundo, e essa soma vai 
					 * ser dividido pelo list.size(), que é o tamanho da lista. 					
					 */
			System.out.println("Average price: " + String.format("%.2f", avg));
			
			Comparator<String> comp = (s1, s2) -> s1.toUpperCase().compareTo(s2.toUpperCase());
			/*
			 * esse comparator é pra uma função que compara dois Strings, no caso eu quero comparar os Strings em
			 * ordem alfabetica, o compareTo é pra comparar, e o toUpperCase pra comprar independente se as letras
			 * é maiusculas ou minusculas.
			 */
			
			List<String> names = list.stream()
					.filter(p -> p.getPrice() < avg)// vou filtar todo mundo que tem o preço abaixo da media.
					.map(p -> p.getName())
					/*
					 * agora eu criei uma nova stream contendo apenas os nomes dos produtos que foram filtrados aqui.
					 */
					.sorted(comp.reversed())
					/*
					 * pra ordernar pego o .sorted
					 * pra eu pegar o nome da cada produto.
					 * a interface Comparator, ela tem um default method que ele retorna o comparator ao inverso
					 * que é o comp.reversed, então se eu fiz um Comparator que ele compara na ordem crescente de String
					 * o Comparator.reversed ele vai ser o comparator que compara na ordem decrescente
 					 */
					.collect(Collectors.toList()); // pra ele transformar essa stream em lista
			
			names.forEach(System.out::println);
			//aqui eu estou usando um Reference Method para o println.

		} catch (IOException e) {
			System.out.println("Error: " + e.getMessage());
		}
		sc.close();
	}
}

===========================================================================

package entities;

public class Product {

	private String name;
	private Double price;
	
	public Product(String name, Double price) {
		this.name = name;
		this.price = price;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Double getPrice() {
		return price;
	}

	public void setPrice(Double price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return name + ", " + String.format("%.2f", price);
	}
}

![exercicio-resolvido](https://user-images.githubusercontent.com/61166475/155026145-1883b64e-49ca-47a8-bb1f-a4abe3b85061.png)
