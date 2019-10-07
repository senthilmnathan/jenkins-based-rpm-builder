pipeline {
	agent {
		node {
			label 'master'
		}
	}
	stages {
		stage('Apache Build') {
			steps {
			    sh '''cd apache24
					  if [ ! -z "$(ls *.bz2)" ]
					  then
						version=$(ls *.bz2 | awk -F'-' '{print $NF}' | awk -F'.tar' '{print $1}')
						rpmbuild -tb "$(ls *.bz2)"						
					  else
					    echo "No Apache Build Today"
					  fi'''
			}
		}
		stage('APR UTIL Build') {
			steps {
			    sh '''cd apr-util
					  if [ ! -z "$(ls *.bz2)" ]
					  then
						version=$(ls *.bz2 | awk -F'-' '{print $NF}' | awk -F'.tar' '{print $1}')
						rpmbuild -tb "$(ls *.bz2)"					
					  else
					    echo "No APR Build Today"
					  fi'''
			}
		}
		stage('Tomcat7 Build') {
			steps {
			    sh '''cd tomcat7
					  if [ ! -z "$(ls *.spec)" ]
					  then
						  if [ ! -z "$(ls *.gz)" ]
						  then
							version=$(ls *.gz | awk -F'-' '{print $NF}' | awk -F'.tar' '{print $1}')
							oldVersion=$(grep ^Version tomcat7.spec | awk '{print $NF}')
							sed -i "0,/${oldVersion}/s//${version}/" tomcat7.spec
							cp -p *.gz /var/jenkins_home/rpmbuild/SOURCES/
							cp -pr *.init *.logrotate $HOME/rpmbuild/SOURCES/
							rpmbuild -bb tomcat7.spec 							
						  else
							echo "No Tomcat7 Build Today"
						  fi
					  else
						  echo "Ensure Spec File is Present in the repository"
					  fi'''
			}
		}
		stage('Tomcat8 Build') {
			steps {
			    sh '''cd tomcat8
					  if [ ! -z "$(ls *.spec)" ]
					  then
						  if [ ! -z "$(ls *.gz)" ]
						  then
							version=$(ls *.gz | awk -F'-' '{print $NF}' | awk -F'.tar' '{print $1}')
							oldVersion=$(grep ^Version tomcat8.spec | awk '{print $NF}')
							sed -i "0,/${oldVersion}/s//${version}/" tomcat8.spec
							cp -p *.gz /var/jenkins_home/rpmbuild/SOURCES/
							cp -pr *.init *.logrotate $HOME/rpmbuild/SOURCES/
							rpmbuild -bb tomcat8.spec 							
						  else
							echo "No Tomcat8 Build Today"
						  fi
					  else
						  echo "Ensure Spec File is Present in the repository"
					  fi'''
			}
		}
		stage('Tomcat9 Build') {
			steps {
			    sh '''cd tomcat9
					  if [ ! -z "$(ls *.spec)" ]
					  then
						  if [ ! -z "$(ls *.gz)" ]
						  then
							version=$(ls *.gz | awk -F'-' '{print $NF}' | awk -F'.tar' '{print $1}')
							oldVersion=$(grep ^Version tomcat9.spec | awk '{print $NF}')
							sed -i "0,/${oldVersion}/s//${version}/" tomcat9.spec
							cp -p *.gz /var/jenkins_home/rpmbuild/SOURCES/
							cp -pr *.init *.logrotate $HOME/rpmbuild/SOURCES/
							rpmbuild -bb tomcat9.spec 							
						  else
							echo "No Tomcat9 Build Today"
						  fi
					  else
						  echo "Ensure Spec File is Present in the repository"
					  fi'''
			}
		}
		stage('Stash RPMs and Cleanup') {
			steps {
				sh '''mkdir -p /var/jenkins_home/RPMs/$(date +%d_%m_%Y)
					  find /var/jenkins_home/rpmbuild/RPMS/ -name '*.rpm' -exec mv -t /var/jenkins_home/RPMs/$(date +%d_%m_%Y) {} +
					  echo -e "All RPM files are stashed under /var/jenkins_home/RPMs/$(date +%d_%m_%Y)"
					  ls -tlr /var/jenkins_home/RPMs/$(date +%d_%m_%Y)/*.rpm
					  find /var/jenkins_home/rpmbuild/ -type f -delete'''
			}
		}
	}
}
