---
layout: post
title: "O Magalhães, mudar para Linux e NixOS"
published: false
---

Em 2008, os meus pais ofereceram-me o meu primeiro computador pessoal: o portátil *netbook* Magalhães, um *rebrand* do Intel Classmate PC, montado em Portugal e distribuído pelos alunos do primeiro ciclo. O Magalhães vinha equipado com um processador Intel Celeron M de 900MHz e com 1GB de memória.[^1] Curiosamente, o Magalhães vinha com dois sistemas operativos instalados, em configuração *dual boot*: Windows XP e Linux Caixa Mágica, uma distribuição Linux portuguesa cuja última versão tem como base o Ubuntu, mas versões mais antigas tiveram como base o Mandriva.[^2] Este sistema didático de código aberto vinha acompanhado de software educativo e videojogos, como o [GCompris][GCompris]{:target="_blank"}, cuja célebre tradução para português estava repleta de erros,[^3] e o SuperTux, um clone do jogo Super Mario Bros.

![Portátil Magalhães](/assets/img/2023-09-10-mudar-para-linux/magalhães.jpg)

### Windows

Durante os três anos em que utilizei o Magalhães, fi-lo quase exclusivamente com o Windows XP. Para mim, o Linux Caixa Mágica era demasiado direcionado para a aprendizagem, e eu estava mais interessado em jogar jogos online e personalizar o desktop.

Sendo assim, naquela altura, o Windows tornou-se rapidamente no meu sistema operativo de eleição. Simplesmente porque julgava-o ser o mais flexível. Desde então, embora tenha experimentado com o Ubuntu em portáteis antigos, nunca pensei em mudar de sistema operativo. Isto é, até há seis meses atrás.

### Minimalismo e Arch Linux

Em março deste ano, decidi tentar "recuperar" um portátil antigo Asus F551MAV, que estava parado em minha casa há algum tempo. Desmontei o computador, limpei a ventoinha e o dissipador de calor, coloquei pasta térmica nova no processador e instalei um SSD para substituir o disco duro que veio com o portátil. Quando chegou a altura de instalar o SO, fiz uma pesquisa no motor de busca: "as melhores distribuições Linux para computadores antigos". O resultado foram dezenas de listas, a maior parte contendo os suspeitos do costume: Lubuntu, Puppy Linux, Linux Lite e antiX. Porém, num tópico do Reddit, um dos comentários sugeria "esquecer a maior parte das 'distribuições *lightweight*' e experimentar antes uma instalação minimal do Debian ou [Arch Linux][Arch Linux]{:target="_blank"}". A palavra minimal intrigou-me, porque, no passado, quando experimentei *distros* supostamente leves, como o Lubuntu ou Linux Mint XFCE, senti que os desenvolvedores desses projetos empacotavam demasiados programas e funcionalidades que eu não utilizava.

Assim, decidi pôr à prova aquela sugestão. Utilizei o archinstall[^4] para particionar o disco e instalar o sistema operativo, e escolhi o perfil Xorg, que não inclui nenhum *desktop environment*, porém inclui os pacotes do servidor gráfico X. A seguir, instalei e configurei o gestor de janelas i3, o lançador de aplicações dmenu e os programas do costume (Firefox, Discord, etc.). A modularidade deste sistema impressionou-me, e a capacidade de incluir apenas os programas que me interessavam foi uma lufada de ar fresco, tendo em conta a tendência para a Microsoft incluir cada vez mais *bloatware* com cada versão do Windows.

Há cerca de um mês e meio, comprei um SSD para poder instalar uma distruibuição Linux no meu portátil principal. Existe software exclusivo para Windows de que não posso prescindir, como é o caso do Ableton Live, então mantive esse sistema no SSD que veio com o computador, utilizando a interface UEFI[^5] para escolher entre Linux e Windows no arranque. No entanto, a distribuição que escolhi não foi nem Debian, nem Arch.

### NixOS

O [NixOS][NixOS]{:target="_blank"} é uma distribuição com base no [Nix][Nix]{:target="_blank"}, um "gestor de pacotes puramente funcional". Isto é, "que trata os pacotes como valores nas linguagens de programação puramente funcionais, como Haskell: esses valores são construídos por funções que não têm 'efeitos secundários' e que nunca mudam depois de terem sido construídos". Ou seja, no caso do Nix, "os pacotes são armazenados no diretório `/nix/store`, onde cada pacote tem o seu próprio subdiretório, que é identificado por um *hash* criptográfico que 'captura' todas as suas dependências". Isto permite aos utilizadores do Nix manter instaladas várias versões e variantes do mesmo software, e, consequentemente, voltar para uma versão mais antiga, se necessário. Para além disso, os pacotes são construídos com o auxílio de [Nix expressions][Nix expressions]{:target="_blank"}, que determinam e declaram as dependências, fontes e o *build script* da maneira mais precisa possível, para garantir que "construir um pacote segundo uma Nix expression tem sempre o mesmo resultado".[^6]

Já o NixOS, aplica este paradigma ao sistema todo. A configuração do SO é declarativa e, por isso, reproduzível. O NixOS é também conhecido por ser um sistema imutável, porque toda a configuração é armazenada no `/nix/store`, que é *read-only*. Isto quer dizer que é impossível editar manualmente as definições do sistema, todas as alterações devem ser feitas a partir do ficheiro `/etc/nixos/configuration.nix`. Para mais informações, recomendo a leitura do artigo *[Overview of the NixOS Linux distribution][Overview]{:target="_blank"}*.

![NixOS](/assets/img/2023-09-10-mudar-para-linux/nixos.jpg)

O ecossistema Nix é altamente complexo, e o que escrevo aqui sobre o mesmo é apenas a ponta do icebergue.[^7] Talvez por isso é que, recentemente, decidi voltar a instalar o Arch Linux.

### O desktop imutável não está pronto

O NixOS é, sem dúvida, o sistema operativo mais interessante que já experimentei. Contudo, há uma razão pela qual me vi obrigado a mudar para o Arch Linux: muitas aplicações pura e simplesmente não funcionam bem num sistema imutável. Ironicamente, e por mais que o Nix seja direcionado para desenvolvedores,[^8] foi precisamente nesse domínio que encontrei o maior número de falhas.

Este blogue utiliza o [Jekyll][Jekyll]{:target="_blank"}, um gerador de *sites* estáticos, escrito em Ruby, que transforma "texto simples", que estou a utilizar para escrever esta publicação, em HTML que um navegador consegue ler. Ora, o Jekyll é um bom exemplo do quão difícil pode ser configurar um ambiente de desenvolvimento em NixOS. Num sistema mutável, preparar um blogue com o Jekyll para ser instalado no GitHub Pages é simples. Mas, no NixOS, é necessário implantar múltiplos *workarounds*.[^9] Aliás, foi justamente a montagem deste blogue que me fez desistir do Nix.

Recomendo a audição de [um excerto do *podcast* Tech Over Tea][Tech Over Tea]{:target="_blank"}, de Brodie Robertson com [Jeremy Soller][Jeremy Soller]{:target="_blank"}, sobre o estado das distribuições imutáveis, as suas vantagens e desvantagens. "Existe uma espécie de brecha entre os utilizadores que estão satisfeitos com o modelo do sistema imutável porque, no dia-a-dia, não se deparam com nenhuma situação que desfavorece o modelo, e os utilizadores com muita experiência que conseguem contornar as lacunas". Eu tendo a concordar, e até sou capaz de admitir que o NixOS é a distribuição que está mais próxima de colmatar essa falha. Ainda assim, para um utilizador como eu, o desktop imutável não está pronto.

![Desktop](/assets/img/2023-09-10-mudar-para-linux/arch+awesome.jpg)

---

#### Notas de rodapé e referências

[^1]: <https://portatilmagalhaes.com/especificacoes-de-hardware-do-portatil-magalhaes>{:target="_blank"}

[^2]: <https://pinguinsmagicos.blogs.sapo.pt/55268.html>{:target="_blank"}

[^3]: Por exemplo, "«Dirije o guindaste e copía o modelo», explicam as instruções de um puzzle" - [Jornal Expresso][Expresso]{:target="_blank"}

[^4]: Lê-se na [ArchWiki][ArchWiki]{:target="_blank"}: "archinstall is a helper library which automates the installation of Arch Linux. It is packaged with different pre-configured installers, such as a 'guided' installer".

[^5]: Alternativa moderna à BIOS, o software de baixo nível que tem como função arrancar o sistema operativo do utilizador.

[^6]: <https://nixos.org/guides/how-nix-works>{:target="_blank"}

[^7]: Faltou mencionar os Nix shell environments, o Home Manager e os Flakes, entre outras funcionalidades.

[^8]: Lê-se no [website do Nix][website do nix]{:target="_blank"}: "Nix provides developers with a complete and consistent development environment. Stop worrying how to install dependencies for your project."

[^9]: <https://matthewrhone.dev/jekyll-in-nixos>{:target="_blank"}


[GCompris]: https://github.com/gcompris/GCompris-qt
[Arch Linux]: https://archlinux.org
[Expresso]: https://expresso.pt/actualidade/magalhaes-tem-tantos-erros-que-e-dificil-contar-los=f501729
[ArchWiki]: https://wiki.archlinux.org
[NixOS]: https://nixos.org
[Nix]: https://nixos.wiki/wiki/Nix_package_manager
[Nix expressions]: https://nixos.wiki/wiki/Overview_of_the_Nix_Language
[Overview]: https://nixos.wiki/wiki/Overview_of_the_NixOS_Linux_distribution
[website do nix]: https://nixos.org/explore.html
[Jekyll]: https://jekyllrb.com
[Tech Over Tea]: <https://youtu.be/ioswlaxdhSA?si=prJg-SU2_BWmo73e&t=3960>
[Jeremy Soller]: https://soller.dev

