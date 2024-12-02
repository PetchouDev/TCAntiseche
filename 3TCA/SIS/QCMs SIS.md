
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

# QCM5 : ...

