 Docker works best for stateless applications that can be ephemeral.
	 - If your application needs to write a file and is dependent on state, perhaps docker is not the best choice.
	 - You can however, externalize the state using an external block file system (AWS EBS)