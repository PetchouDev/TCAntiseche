

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
1. Q
2. Q
3. Q
4. Q
5. Q
6. Q
7. Q
8. Q
9. Q
10. Q
11. Q


# QCM 8 : Réponse fréquentielle

1. Q
2. Q
3. Q
4. Q
5. Q
6. Q
7. Q
8. Q
9. Q
10. Q
11. Q

# QCM 9 : transformée en Z
1. Q
2. Q
3. Q
4. Q
5. Q
6. Q
7. Q
8. Q
9. Q
10. Q
11. Q




