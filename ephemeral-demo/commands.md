k exec -it pause-deployment-5df97c5fff-j2gkf -- sh # this should fail

k debug -it pause-deployment-5df97c5fff-j2gkf --image=busybox:latest \
--target=pause # this should work