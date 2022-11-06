k exec -it pause-deployment-/<ID/> -- sh # this should fail

k debug -it pause-deployment-/<ID/> --image=busybox:latest \
--target=pause # this should work
