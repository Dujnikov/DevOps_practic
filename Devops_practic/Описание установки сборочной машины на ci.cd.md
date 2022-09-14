https://docs.gitlab.com/runner/install/bleeding-edge.html#download-any-other-tagged-release - релизы версий для установки 

Прописать в visudo

gitlab-runner   ALL=(ALL:ALL) NOPASSWD: ALL
aeca            ALL=(ALL:ALL) NOPASSWD: ALL
Чтобы выполгнение было без введения пароля