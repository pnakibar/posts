# Tutorial de Selenium WebDriver Para Scala/Java utilizando SBT
## Autor: Pedro Mathias Nakibar


### Observações
Utilizei a linguagem Scala para fazer o teste pois é minha principal linguagem de desenvolvimento. O código estará todo *idiomático* em Java, pois a biblioteca é nativamente feita para Java. Estou apenas utilizando Scala pela facilidade, ser menos verbosa que Java. Porém o código é muito parecido nos dois.

### 0. Baixando o pacote
Estou utilizando o SBT, gerenciador de pacotes padrão do Scala e utilizando build.sbt para controlar os meus pacotes, portanto, é só adicionar está linha 

```scala
	libraryDependencies += "org.seleniumhq.selenium" % "selenium-java" % "2.48.2"
```

que está tudo feito, caso você utilize Maven ou outro gerenciador de pacotes, [veja no mvn repositorycomo insere ele no seu Maven, ou Gradle...](http://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java/2.48.2).

### 1. Hello World!
O código é bem simples:

```scala
import org.openqa.selenium.firefox.FirefoxDriver

/**
  * Created by pnakibar on 10/12/15.
  */
object Main extends App{
  val driver = new FirefoxDriver //instancia o driver do firefox
  driver get "http://www.google.com" //realiza um *get* na página do google

  println (driver getTitle) //pega o nome da página que está em aberto no driver/navegador e imprime

  driver quit

}
```

### 2.A página
Dentro do objeto driver que foi instanciado acima, temos vários metódos disponiveis que permitem navegar pela página, acessando cada componente do HTML de maneira fácil e rápida.

O metódo *driver.findElement(...)* (e sua variantes, como *driver.findElementByName("...")*) todos retornam um objeto do tipo *WebElement*, que possui metódos que permite que aquele componente da página de maneira fácil e rápida:
* Clear: Limpa um campo de text
* Click: Simula um *click* do mouse
* FindElement e FindElements: Busca por elementos que são filhos o elemento pai
* SendKeys: Envia apertos de teclas para o elemento
* *para mais consulte a documentação ou o código fonte, ou o auto-complete da sua IDE (haha)*

Caso um elemento não seja achado ele irá disparar uma exceção, conforme mostro abaixo. Isso é extramemente interessante caso você faça testes que involvam páginas que gerem código.

Extendendo o exemplo 1, o código abaixo entra no google e busca por *alguma coisa* e busca pelo botão de procurar e aperta ele e por fim imprime a URL:

```scala
import org.openqa.selenium.firefox.FirefoxDriver

/**
  * Created by pnakibar on 10/12/15.
  */
object Main extends App{
  val driver = new FirefoxDriver
  driver get "http://www.google.com"

  val searchText = driver.findElementById("lst-ib") //busca pelo campo de inserir texto
  searchText.sendKeys("Alguma coisa") //preenche esse campo com a string "Alguma coisa"

  driver.findElementByName("btnK").click() //busca pelo botão "btnK" que é o botão de *Procurar*

  println (driver getCurrentUrl)


  println("opened!")

  driver quit
}

```

Porém, o código acima irá disparar uma exceção, pois a página de pesquisa do Google automaticamente te *transfere* para outra quando você digita algum texto, para *corrigir* isso, basta colocar um **Try** na requisição em que ele busca pelo botão de ok. O navegador funciona lado a lado com o seu código, portanto, deve sempre se tomar cuidado quando você fizer certas requisições a **API** do Selenium, que involvam uma mudança no estado que você não está preparado para tratar, como no exemplo acima, o componente sumir.

### 4.Preenchendo um formulário

### 5.Baixando um recurso


#TODO:
* Falar sobre comandos driver.next(), driver.refresh(), etc.
		
