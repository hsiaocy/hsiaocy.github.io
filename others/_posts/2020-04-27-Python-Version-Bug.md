---
image: 
  teaser: others.jpg

layout: article
title: Python Version Bug
date: 2020-04-27
categories: notes
author: chunyi_hsiao
tags: [Python, Troubleshooting]
share: true
---

- **Exception**:
	- Similar problem: [link](https://github.com/pypa/pip/issues/6251)
	- The ValueError raised after typed  
		```pip3 freeze > requirements.txt>``` 

		and it gave: 
		```FileNotFoundError: [Errno 2] No such file or directory: '/home/user/anaconda3/lib/python3.6/site-packages/psutil-5.4.8.dist-info/METADATA'```
		
		Output:
		<pre class="brush: bash">
		Error checking for conflicts.
		Traceback (most recent call last):
		File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2897, in _dep_map
			return self.__dep_map
		File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2691, in __getattr__
			raise AttributeError(attr)
		AttributeError: _DistInfoDistribution__dep_map
		\n
		During handling of the above exception, another exception occurred:
		\n
		Traceback (most recent call last):
		File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2888, in _parsed_pkg_info
			return self._pkg_info
		File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2691, in __getattr__
			raise AttributeError(attr)
		AttributeError: _pkg_info
		\n
		During handling of the above exception, another exception occurred:

		Traceback (most recent call last):
			File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_internal/commands/install.py", line 503, in _warn_about_conflicts
				package_set, _dep_info = check_install_conflicts(to_install)
			File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_internal/operations/check.py", line 108, in check_install_conflicts
		    	package_set, _ = create_package_set_from_installed()
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_internal/operations/check.py", line 47, in create_package_set_from_installed
		    	package_set[name] = PackageDetails(dist.version, dist.requires())
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2635, in requires
		    	dm = self._dep_map
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2899, in _dep_map
		    	self.__dep_map = self._compute_dependencies()
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2908, in _compute_dependencies
		    	for req in self._parsed_pkg_info.get_all('Requires-Dist') or []:
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 2890, in _parsed_pkg_info
		    	metadata = self.get_metadata(self.PKG_INFO)
	    	File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 1410, in get_metadata
		    	value = self._get(self._fn(self.egg_info, name))
    		File "/home/jwfu/anaconda3/lib/python3.6/site-packages/pip/_vendor/pkg_resources/__init__.py", line 1522, in _get
		    	with open(path, 'rb') as stream:
		FileNotFoundError: [Errno 2] No such file or directory: '/home/jwfu/anaconda3/lib/python3.6/site-packages/psutil-5.4.8.dist-info/METADATA'
		</pre> 

	- Stackoverflow question [link](https://stackoverflow.com/questions/54454367/different-error-messages-when-using-pip-install-pip-list-ect)

- **root cause explanation**: reffered to [here](https://github.com/pypa/pip/pull/6225).

- **howto fix**: 
	1. for each folder that starts with "-", delete it and reinstall the corresponding package.
	2. modify in **/src/pip/_internal/utils/temp_dir.py**   
		```LEADING_CHARS = "-~.+=%0123456789"```
		-> ```LEADING_CHARS = "~.=%0123456789"```
