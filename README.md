The idea is to create a Jenkins Continuous Integration (CI) Pipeline To Trigger Automatically on GitHub Pull Requests , The Jenkins server will be on an EC2 instance! 

![Capture d'écran 2024-09-02 224223](https://github.com/user-attachments/assets/c2055c1a-7075-4697-9219-81dc36ddaf46)

First step is to access EC2 instance through SSH and install Java and maven 
Then install Jenkins on the instance following the instructions here : https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/#creating-a-key-pair

Then Accessing Jenkins Dashboard using public EC2 instance ip 

![Capture d'écran 2024-09-02 224223](https://github.com/user-attachments/assets/6f5e2341-4446-462f-bdb4-78f8ac7be965)

Then on the Jenkins Server : 
1) Install GitHub pull Request Builder Plugin : 

![Capture d'écran 2024-09-02 203347](https://github.com/user-attachments/assets/f69ab40b-7dfc-4f69-bed2-a5b51c014111)

Then Create a acces token from github to use it on the plugin , 

Note that the credentials of the plugin should be a secret text type containing the .pem Key used to acces EC2 instance through SSH !

![Capture d'écran 2024-09-02 204046](https://github.com/user-attachments/assets/ac4b1a12-6264-4429-a827-347aff69f700)

*connections tests for credentials and  with github and github repo should be successful*

2) Creating GitHub Webhook :

![Capture d'écran 2024-09-02 210251](https://github.com/user-attachments/assets/5320b44d-eb4f-4d71-9d8d-8da06829b4c0)

the payload should be the public ec2 instance + /ghprbhook

The secret should be taken from the github pull request builder plugin 

![Capture d'écran 2024-09-02 205457](https://github.com/user-attachments/assets/219f3ce4-4fcd-4ad0-8b95-80836257fd11)

Then Configuring the webhook to trigger on pull requests

![Capture d'écran 2024-09-02 205845](https://github.com/user-attachments/assets/c9c48375-d0d5-4069-8052-0bb845795a9a)

Making sure the webhook is successfuly connected to the jenkins server : 

![Capture d'écran 2024-09-02 211254](https://github.com/user-attachments/assets/624ece63-77a4-4586-9202-2f1879c65627)

3) Creating the jenkinsfile for the CI script :

![Capture d'écran 2024-09-02 212006](https://github.com/user-attachments/assets/b787a285-693a-49ee-a4f7-fb59d1e5fe4b)

4) Creating a Pipeline :

![Capture d'écran 2024-09-02 212512](https://github.com/user-attachments/assets/ca459f0c-7cb9-4506-9c3d-764d17fb7e13)

![Capture d'écran 2024-09-02 212604](https://github.com/user-attachments/assets/7bb31339-7077-4954-a6a2-ee8a83845641)

![Capture d'écran 2024-09-02 212658](https://github.com/user-attachments/assets/6a30cc94-f2f0-499c-8a00-d479a2fba86a)

![Capture d'écran 2024-09-02 212710](https://github.com/user-attachments/assets/6bd18c3d-c687-4f68-84dd-a83cd810e599)

![Capture d'écran 2024-09-02 212725](https://github.com/user-attachments/assets/8d811977-d73d-419c-b128-0220a23c965e)

![Capture d'écran 2024-09-02 215739](https://github.com/user-attachments/assets/2768c6f9-8030-4676-8ae2-8a552af5ea45)

*credentials should be the username of github + access token we just generated!*

![Capture d'écran 2024-09-02 215749](https://github.com/user-attachments/assets/b9c4761d-5dc9-4891-a71d-fdaac153869a)

*Script path should be the exact name of the jenkinsfile since its in the main repo*

Then testing the pipeline : 

![Capture d'écran 2024-09-02 220106](https://github.com/user-attachments/assets/dff01048-03bf-45ab-8464-41a58036db36)

5) Creating another branch to test the pull request :

![Capture d'écran 2024-09-02 220527](https://github.com/user-attachments/assets/0d9284b5-7faf-45ee-a7f9-45182f6a86e9)

![Capture d'écran 2024-09-02 220605](https://github.com/user-attachments/assets/a419f0f4-e4d0-4498-bdbf-e27f12628240)

*modifying the README.md in the testing-ci branch*

commiting the changes and pushing to github : 

![Capture d'écran 2024-09-02 220833](https://github.com/user-attachments/assets/fbe75034-0f36-44e5-939b-bbee5265a547)

![Capture d'écran 2024-09-02 230917](https://github.com/user-attachments/assets/de6b0fe3-d51d-4d8f-88a7-40ec5d2bce8b)

6) Testing the pull request :

![Capture d'écran 2024-09-02 221821](https://github.com/user-attachments/assets/04d36b7d-b46f-49eb-b65c-78a35b6f7433)

*new changes*

CI pipeline Working succesfuly and automated a Build !

![Capture d'écran 2024-09-02 222046](https://github.com/user-attachments/assets/96563851-ea54-49b6-91e8-45078870e0b0)

Merge now have no conflicts since the build is successfull!


*END*

