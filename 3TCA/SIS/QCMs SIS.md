

# QCM 1 : Chaine de traitement numérique

1. Sélectionner les propositions correctes.![[QCM1Q1.png]]
   
2. Sélectionner les proposition correctes.   ![[QCM1Q2.png]]
   
3. On considère la chaine de traitement numérique réalisée par un système de transmission. Sélectionner les propositions correctes.![[QCM1Q3.png]]
   
4. On considère la chaine de traitement numérique réalisée par une carte son d'un ordinateur. Sélectionner les propositions correctes.![[QCM1Q4.png]]

# QCM 2 : Signaux 
1. Cocher les affirmations correctes.![[QCM2Q1.png]]
2. A quelle version correspond le signal inconnu ?
   ![[QCM2Q2.png]]
3. Soit un signal discret x qui  prend les valeurs suivantes : x=[1 2 3 0 -1 -2]. L'autocorrélation du signal x est égale à :
   ![[QCM2Q3.png]]
4. La fonction d'autocorrélation d'un signal de durée finie permet de mesurer :
   ![[QCM2Q4.png]]
5. On multiplie un signal continu apériodique $x(t)$ par un peigne de Dirac $\sum_{n=-\infty}^{+\infty} \delta (t-nT)$. Quel est le signal obtenu $y(t)$ ? Quelle est l'opération effectuée par cette multiplication ?  
   ![[QCM2Q5.png]]
6. Déterminer $Rx1x2(\tau)$, l'inter-corrélation de $x_1(t)$ avec $x_2(t)$ représentés ci-dessous :
   ![[QCM2Q6.png]]
7. Quelle est l'expression de $y(t)$ ?
   ![[QCM2Q7.png]]
8. On convolue un signal continu apériodique $x(t)$ de durée T par un peigne de Dirac $\sum_{n=-\infty}^{+\infty} \delta (t-nT)$. Quelle est le signal obtenu $y(t)$ ? Quelle est l'opération effectuée par cette convolution ?
   ![[QCM2Q8.png]]



# QCM 3 : échantillonnage 

1. Soit $x(t)$ un signal de bande limité telle que : $X(f) = 0$ pour $|f| > f_M$. On choisit une fréquence d'échantillonnage $Fe = f_M$. 
   ![[QCM3Q1.png]]
2. Le signal $x(t)$ est échantillonné avec une période d'échantillonnage $T_e$. On obtient le signal $x_e(t)$.
   ![[QCM3Q2.png]]
3. Un signal continu apériodique a une fréquence minimale de 1kHz et une fréquence maximale de 4kHz.   ![[QCM3Q3.png]]
4. Echantillonner en fréquence c'est  : 
   ![[QCM3Q4.png]]

# QCM 4 : Matlab

1. Soit un signal périodique de période T en temps continu, constant et égal à 1 pendant une durée $\alpha = 0.25s$. On trace le spectre des $T \times |X_k|$ pour différentes valeurs de la période ($X_k$: le coefficient de Fourrier de rang k). Associer chacun des spectres à la valeur de la période correspondante.
   ![[QCM4Q1.png]]
2. Voici le début d'un script Matlab
   ```
   N=Fs*T;
   n=0:N-1;
   td=n*Ts;
   F0=2
   T=1
   syms t
   ```
   La suite des instructions est donnée ci-dessous. Relier les bonnes réponses.
   ![[QCM4Q2.png]]
3. On veut créer le vecteur `x` suivant sous Matlab :
   ```
   x = 1 3 5 7 9
   ```
   Sélectionner les instructions permettant de créer le vecteur.
   
   ![[QCM4Q3.png]]
4. Soit l'instruction suivante :
   ```
   [msg_decode, lag]=xcorr(code_x1,code_x1)
   ```
   ![[QCM4Q4.png]]

# QCM5 : séries de Fourrier

1. Soit $x(t)$ un signal périodique de puissance finie, de période T. Soit P sa puissance moyenne.
   ![[QCM5Q1.png]]
2. Soit $x_(t)$ un signal réel et périodique de période T=5ms, de valeur moyenne égale à 1V, d'amplitude max de 2V. On considère sa décomposition en Série de Fourrier réelle à l'aide de coefficients de Fourrier ak et bk.
   ![[QCM5Q2.png]]
3. Soit $x_(t)$ un signal périodique réel de puissance finie, de période T. Soit P sa puissance moyenne.
   ![[QCM5Q3.png]]
4. Soit un signal de durée finie T, correspondant au motif fondamental du signal périodique $x_p(t)$.
   ![[QCM5Q4.png]]

# QCM 6 : CFT
1. Choisir les propositions correctes.
   ![[QCM6Q1.png]]
2. Enoncé simplifié du théorème de Parseval pour un signal à énergie finie.
   ![[QCM6Q2.png]]
3. La transformée de Fourrier ayant pour expression : $2+e^{-j\omega}+0.5e^{-j2\omega}$ peut correspondre au signal temporel :
   ![[QCM6Q3.png]]
4. La transformée de Fourrier d'un signal temps-continu et d'énergie finie suivante :
   $X(f) = \int_{-\infty}^{+\infty}x(t)e^{-j2\pi ft}dt$  
   ![[QCM6Q4.png]]
5. Le spectre d'un signal temps-continu périodique de puissance finie est :
   ![[QCM6Q5.png]]
6. Soit $X(j\omega)$ la transformée de Fourrier du signal $x(t)$. La dérivée du signal $x(t)$ a pour transformée de Fourrier :
   
   ![[QCM6Q6.png]]
7. Un signal temps-continu d'énergie finie a un spectre :
   ![[QCM6Q7.png]]
8. La transformée de Fourrier inverse d'un signal temps-continu est la suivante :
   $x(t) = \int_{-\infty}^{+\infty}X(f)e^{j2\pi ft}df$ 
   ![[QCM6Q8.png]]
9. La transformée de Fourrier inverse d'un signal temps-continu est la suivante :
   $x(t) = \frac{1}{2\pi} \int_{-\infty}^{+\infty} X(j\omega)exp(-j\omega)d\omega$

   ![[QCM6Q9.png]]
10. la transformée de Fourrier d'un signal temps-continu et d'énergie finie est la suivante :
    $X(j\omega) = \int_{-\infty}^{+\infty}x(t)e^{-j\omega t}dt$ 
    ![[QCM6Q10.png]]
11. Choisir les réponses correctes
    ![[QCM6Q11.png]]

# QCM 7 : convolution
1. Soit un STLI causal et initialement au repos de réponse impulsionnelle h, en entrée le signal x et en sortie le signal y. Cocher les propriétés valides :
   ![[QCM7Q1.png]]
2. Soit un signal discret x qui prend les valeurs suivantes : `x=[-1 1 1 -1`
   Soit un STLI initialement au repos dont la réponse impulsionnelle h de durée finie prend les valeurs suivantes : `h=[1 -1 1 -1]`
   Le résultat du filtrage de x par h est :
   ![[QCM7Q2.png]]
3. En temps continu, la réponse $y(t)$ d'un STLI caractérisé par sa réponse impulsionnelle $h(t)$, lorsque l'on applique une entrée $x(t)$ s'obtient par l'opération suivante : 
   $y(t_0) = \int_{-\infty}^{+\infty}x(t_0-\tau)h(\tau)d\tau$ 
   ![[QCM7Q3.png]]
4. Quelle est la sortie d'un SLTI initialement au repos lorsque rentrée appliquée x\[n] et la réponse impulsionnelle h\[n] sont les signaux représentés ci-dessous :
   ![[QCM7Q4.png]]
5. L'opération de convolution
   ![[QCM7Q5.png]]
6. En temps discret, la réponse y\[n] d'un SLTl caractérisée par sa repanse impulsionnelle lorsqu'on applique une entrée x\[n] s'obtient par l'opération suivante :
   $y[k] = \sum_{k=-\infty}^{+\infty} x[n]h[k-n]$ 
   ![[QCM7Q6.png]]
7. Soient deux signaux $x(t)$ et $y(t)$ que l'on va convoluer :
   $z(t) = x(t) * y(t)$
 ![[QCM7Q7.png]]
8. En temps continu, la réponse $y(t)$ d'un SLTI caractérisé par sa réponse impulsionnelle $h(t)$, lorsqu'on applique ure entrée $x(t)$ s'obtient par l'opération suivante :
   $y(t) = \int_{-\infty}^{+\infty}x(t-\tau)h(\tau)$  
   ![[QCM7Q8.png]]
9. En temps discret, la réponse d'un SL Tl caractérise par sa réponse impulsionnelle $h[n]$, lorsqu'on applique une entrée x\[n] s'obtient par l'opération suivante :
	$y[n] = \sum_{k=-\infty}^{+\infty}x[k]h[n-k]$  
   ![[QCM7Q9.png]]
10. Soit un SLTI causal, stable et initialement au repos de réponse impulsionnelle h, en entrée le signal x et en sortie le signal y, cochez les expressions correctes :
    
    ![[QCM7Q10.png]]
11. Soit un signal discret x qui prend les valeurs suivantes :
    `x=[1 2 3 2 1]`
    Soit un SLTI initialement au repos dont la réponse impulsionnelle h de durée finie prend les valeurs suivantes :
	`h=[1 -1]`
	Le résultat du filtrage de x par h est :
    ![[QCM7Q11.png]]


# QCM 8 : Réponse fréquentielle

1. Associer les diagrammes de Bode à leur réponse fréquentielle.
   ![[QCM8Q1P1.png]]
	![[QCM8Q1P2.png]]
2. On considère la forme canonique d'un système du 2nd ordre en temps continu.
   ![[QCM8Q2.png]]
3. Sélectionner les affirmations correctes.
   ![[QCM8Q3.png]]
4. Cochez le(s) réponse(s) en fréquences qui peuvent donner ce diagramme de Bode :
   ![[QCM8Q4.png]]
5. Soit la réponse impulsionnelle h\[n] d'un filtre numérique :
   ![[QCM8Q5.png]]
6. Dans les affirmations suivantes concernant les systèmes au 1er ordre, sélectionner celles qui sont correctes.
   ![[QCM8Q6.png]]
7. On considère la forme canonique d'un système du 1er ordre, sélectionner les affirmations qui sont correctes.
   ![[QCM8Q7.png]]
8. Choisir les bonnes réponses 
   ![[QCM8Q8.png]]
9. Soit un système du 2nd ordre défini par l'équation aux différences suivante :
   $y[n]-2rcos(\theta)y[n-1]+r^2y[n-2]=x[n]$ 
   ![[QCM8Q9.png]]
10. Sélectionner les affirmations correctes.
    ![[QCM8Q10.png]]
11. Associer les diagrammes de Bade à leur réponse fréquentielle.
    ![[QCM8Q11P1.png]]
    ![[QCM8Q11P2.png]]
    ![[QCM8Q11P3.png]]

# QCM 9 : transformée en Z
1. Soient deux systèmes temps discret notés S1 et S2 qui ont respectivement h1\[n] et h2\[n]) comme réponse impulsionnelle et H1(z) et H2(z) comme fonction de transfert.
   La réponse impulsionnelle de SI est donnée ci-après :
   ![[QCM9Q1P1.png]]
   ![[QCM9Q1P2.png]]
2. Parmi les réponses ci-après, quelle(s) est (sont) celle(s) correspondante(s) à la transformée en Z du signal x\[n] suivant?
   x\[n] = 1 si n = -2
   x\[n] = -1/2 si n = -1
   x\[n]= -1 si n = 0
   x\[n] = 1/2 si n = 1
   x\[n] = 0 ailleurs
   ![[QCM9Q2.png]]
3. Soit le système causal décrit par l'équation aux différences suivante :
    $y[n] — 0.5y[n-1] = x[n]$.
    Le système est initialement au repos.
    On applique à rentrée x\[n] = $\alpha. u [n]$ avec $\alpha \in \mathbb{R}$. 
    Cocher les propositions correctes.
   ![[QCM9Q3.png]]
4. Soit un SLTI discret caractérisé par l'équation : $y[n] - \frac{1}{2} y[n-1]=x[n] + \frac{1}{3}x[n-1]$ 
   Quelle est la fonction de transfert $H(z)$ ?
   Quels sont les zéros et les pôles de ce SLTI ?
   Que faut-il pour assurer la stabilité de ce SLTI ?
   ![[QCM9Q4.png]]
5. Le schéma bloc suivant défini le système S causal :
   ![[QCM9Q5.png]]
6.  Parmi les réponses ci-après, quelle(s) est (sont) celle(s) correspondante(s) à la transformée en Z du signal x\[n] suivant ?
   x\[n] = 1 si n = 2
   x\[n] = -1/2 si n = 1
   x\[n]= -1 si n = 0
   x\[n] = 1/2 si n = -1
   x\[n] = 0 ailleurs
   
   ![[QCM9Q6.png]]
7. Trois fonctions de transfert $H_i(z)$ avec $i\in[1;3]$ sont représentées par leur diagramme zéros/pôles.
   (K=1 dans l'écriture factorisée de $H_i(z)$ à l'aide des zéros et des pôles)
   Associer chaque fonction de transfert $H_i(z)$ au module de la réponse fréquentielle qui lui correspond.
   ![[QCM9Q7.png]]
8. Soit un système temps discret noté S1 qui a h1\[n] comme réponse impulsionnelle et H1(z) comme fonction de transfert.
   La réponse impulsionnelle de S1 est donnée ci-après:
   Cocher les bonnes réponses.
   ![[QCM9Q8.png]]
9. Six fonctions de transfert $H_i(z)$ avec $i\in[1;6]$ sont représentées par leur diagramme zéros/pôles.
   (K=1 dans l'écriture factorisée de $H_i(z)$ à l'aide des zéros et des pôles)
   Associer chaque fonction de transfert $H_i(z)$ au module de la réponse fréquentielle qui lui correspond.
   ![[QCM9Q9P1.png]]
   ![[QCM9Q9P2.png]]
10. Soit le système causal décrit par l'équation aux différences suivante :
    $y[n]+3y[n-1]=x[n]$
    Le système est initialement au repos.
    On applique à l'entrée $x[n]=\alpha.u[n]$ avec $\alpha \in \mathbb{R}$. 
    Cocher les propositions correctes.
    ![[QCM9Q10.png]]
11. Soit le système causal décrit par l'équation aux différences suivante :
    $y[n] — 0.5y[n-1] = x[n]$.
    Le système est initialement au repos.
    On applique à rentrée x\[n] = $\alpha. u [n]$ avec $\alpha \in \mathbb{R}$. 
    Cocher les propositions correctes.
    ![[QCM9Q11.png]]
12. Le schéma bloc suivant défini le système S causal :
    ![[QCM9Q12.png]]


En espérant que ça vous aide. ❤️ sur vous la team.

