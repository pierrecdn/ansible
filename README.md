# docker-ansible

Run [Ansible](http://ansible.com) from inside a container.

Learn how to use Ansible on [http://docs.ansible.com/ansible/index.html]

![Ansible logo](https://upload.wikimedia.org/wikipedia/commons/0/05/Ansible_Logo.png)

## How to use this Docker image

* Simple use-case : 

```bash
$ docker run -ti --rm -v <your_rsa_key>:/root/.ssh/id_rsa:ro -v <your_playbooks_root>:/etc/ansible:ro pierrecdn/ansible ansible-playbook -i <inventory_file> <playbook_file>

PLAY [your-hostgroup] *********************************************************

GATHERING FACTS *************************************************************** 
ok: [host-1]
ok: [host-2]
ok: [host-3]

TASK: [task-1 | My task to rule the world] ************************************ 
(...)
```

## Advices and remarks

* Take care of integrity of your files: use :ro when mouting volumes, no reason for ansible to write anything. 

* Ansible has no real context over 2 subsequent executions, so it can be reinstantiated each time. That's why containerize it and passing --rm it's not a problem. 

* If you plan to use Docker on the local instance, you will probably face a problem. Look at [jpetazzo/dind](https://github.com/jpetazzo/dind) first.

* Remark : this image is shipped with pip and [docker-py](https://github.com/docker/docker-py) (See [here](http://docs.ansible.com/ansible/docker_module.html) for the features it enable)

