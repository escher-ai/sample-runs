CURRENT_BRANCH=`git branch | grep \* | cut -d ' ' -f2`
RUN_BRANCH=escher-run-$${RUN_ID}
RUN_REPO_URL=https://github.com/escher-ai/sample-runs.git

default:
#	make clean
	make run
clean:
	rm -rf /tmp/tensorflow/pendulum-v0
start-tensorboard:
	tensorboard --logdir=/tmp/tensorflow
run:
	bash -c "source activate gym && \
	RUN_ID=$$(date +'%Y%m%d-%H%M%S') \
	DISPLAY=:1.0 python policy_gradient.py"
test:
	echo $(RUN_BRANCH)
	sleep 2
	echo $(RUN_BRANCH)
setup-escher-remote:
	git remote add escher $(RUN_REPO_URL)
pre-run:
	CURRENT_BRANCH=$(CURRENT_BRANCH) && \
	RUN_ID=$$(date +'%Y%m%d-%H%M%S') \
	RUN_BRANCH=$(RUN_BRANCH) && \
	git co -b $${RUN_BRANCH} && \
	git add . && \
	git commit -m $$RUN_BRANCH} && \
	git push escher $(RUN_BRANCH) -f && \
	git co master && \
	git merge --no-commit --squash ${RUN_BRANCH} && \
	git reset HEAD # to unstage the changes
