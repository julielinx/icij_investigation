# icij_investigations
Analysis and ML of the ICIJ investigations - panama papers, paradise papers, offshore leaks, bahamas leaks

When cloning the repo with git clone gitrepoURL, if error message received:
- fatal: unable to access gitrepoURL: SSL certificate problem: self signed certificate in certificate chain

Use the following command:
- git -c http.sslVerify=false clone gitrepoURL
