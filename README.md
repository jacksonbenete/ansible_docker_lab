# Ansible Lab

### Using the Lab
Start your lab network by running:
```ash
docker-compose up
```

Jack into the control-node to start using Ansible:
```ash
docker exec -it control.node bash
```

You can ping all nodes using:
```ash
ansible all -m ping
```

If you can ping the containers successfully, our nodes are running.

But you can check that we still can't access our web servers.

Using curl or a browser request [`localhost:8081`](http://localhost:8081) for node1 (or 8082 for node2) and check that it fails to render a web page.

We can run a Play to install Nginx in all servers:
```ash
ansible-playbook someplaybook.yml
```

Example of a Play that receives parameters:
```ash
ansible-playbook find_file.yml -e file_name="foo"
```

Example of a Play that uses an abstraction to call other Plays:
```ash
ansible-playbook abstraction.yml -e process_name="SIX-STREAM"
```

List of useful Plays:
- clone_existing_repo     (used to backup the psrv state in git)
- iterate_over_dict       (used in many horizon pipelines)
- dict_to_list_and_diff   (used in rebuild script and algoserver-aos config)

The Play should install Nginx and start the service on all nodes.

You can now go to [`localhost:8081`](http://localhost:8081) in your browser or port 8082 and check that it works.
