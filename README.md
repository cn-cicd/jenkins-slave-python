# Jenkins Slave Python #

Jenkins Slave for Python builds. Docker image based on official image for Python distribution.

	https://hub.docker.com/r/jnonino/jenkins-slave-python/

## Docker Image Tags ##

-	[`latest` (*latest/Dockerfile*)](https://bitbucket.org/jnonino-devops-cloud/jenkins-slave-python/src/master/latest/Dockerfile)
-	[`3.7-alpine` (*3.7-alpine/Dockerfile*)](https://bitbucket.org/jnonino-devops-cloud/jenkins-slave-python/src/master/3.7-alpine/Dockerfile)
-	[`2.7-alpine` (*2.7-alpine/Dockerfile*)](https://bitbucket.org/jnonino-devops-cloud/jenkins-slave-python/src/master/2.7-alpine/Dockerfile)

## Tools Installed ##

- Python
- Open Java JRE 8
- Git
- Subversion
- Mercurial
- wget
- curl
- unzip
- OpenSSH
- CA Certificates

## Add certificate to connect to HTTPS repositories

To add custom certificates and root CAs, create a new Dockerfile and import them with the following code.

	FROM jnonino/jenkins-slave-python
	LABEL maintainer="Julian Nonino <noninojulian@gmail.com>"

	# Trust Root CA
	COPY Root_CA.crt /tmp
	RUN keytool -importcert -alias Root_CA -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass changeit -file /tmp/Root_CA.crt -noprompt && \
		cp /tmp/Root_CA.crt /usr/local/share/ca-certificates/ && \
		chmod 644 /usr/local/share/ca-certificates/Root_CA.crt && \
		update-ca-certificates

	CMD ["/bin/bash"]