## Développement local 

Si vous travaillez sur votre ordinateur local, vous pouvez suivre ces étapes pour configurer votre environnement afin d’utiliser les labos.  

### C++ Redistributable 
1. Téléchargez et installez [Visual C++ Redistributable (x64)](https://aka.ms/vs/16/release/vc_redist.x64.exe) 

### Python et packages requis 
1. Installez [Python 3.6.1](https://www.python.org/downloads/release/python-361/)  
   - **Important** : Sélectionnez les options pour ajouter Python à la variable PATH et pour l’enregistrer comme environnement Python par défaut. 
2. Après l’installation, ouvrez l’*Invite de commande* et saisissez la commande suivante pour installer les packages nécessaires : 

> pip install ipython jupyter matplotlib pillow requests azure-cognitiveservices-vision-computervision azure-cognitiveservices-vision-customvision azure-cognitiveservices-vision-face azure-cognitiveservices-language-textanalytics azure.cognitiveservices.speech azure_ai_formrecognizer 

### Visual Studio Code 
1. Si Visual Studio Code n’est pas encore installé sur votre système, [téléchargez-le ici](https://code.visualstudio.com/Download). Après l'installation, démarrez Visual Studio Code et dans l'onglet Extensions (CTRL+SHIFT+X), recherchez et installez l'extension **Python** de Microsoft.

2. Dans Visual Studio Code, ouvrez un nouveau Terminal, saisissez **git clone https://github.com/MicrosoftLearning/AI-900FR-Microsoft-Azure-AI-Fundamentals** et sélectionnez *Enter*. 

