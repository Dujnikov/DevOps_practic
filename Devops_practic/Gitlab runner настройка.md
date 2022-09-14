     Установка вручную
	 curl -LJO "https://gitlab-runner-downloads.s3.amazonaws.com/latest/rpm/gitlab-runner_amd64.rpm"
	 
	 dnf install ./gitlab-runner_amd64.rpm

	sysytemctl status gitlab-runner
	
	sudo chmod +x /usr/local/bin/gitlab-runner - права на выполнение
	
	sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash - создание пользователя для ci
	
	sudo gitlab-runner register
	
	https://docs.gitlab.com/runner/install/bleeding-edge.html#download-any-other-tagged-release - релизы версий для установки 
	
	
	
	
	
	gitlab-runner list – показыает существующие раннеры

	gitlab-runner verify – показывает живые раннеры	

	Если возникает ошибка и Runner не может сделать job (Preparation failed: getwd: getwd: no such file or directory) необходимо убить pid рабочего процесса раннера
	ps -ax | grep gitlab-runner - просмотр процессов gitlabrunner
	
	Остановите свой бегун ( `gitlab-runner stop`), а затем запустите его с [флагом отладки](https://gitlab.com/gitlab-org/gitlab-runner/blob/master/docs/faq/README.md#run-in-debug-mode) , чтобы вы могли видеть все, что он делает:

`gitlab-runner --debug run`

	И начните кормить его работой.