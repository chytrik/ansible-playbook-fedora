Ansible playbook: Post Fedora workstation installation 
=========
Post Fedora installation Ansible script for provisioning dev machine.

## Installation
1. Install Ansible:
```
sudo dnf install python-pip
pip install ansible
```
2. To execute the playbook:
```
ansible-playbook -i inventory.ini local.yml --ask-become-pass
```

### Optional:
```
pip install ansible-navigator
```

## Note
If you are using Fedora ARM architecture, you may encounter an error when installing ansible-navigator.
```
...
Building wheels for collected packages: onigurumacffi
  Building wheel for onigurumacffi (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Building wheel for onigurumacffi (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [29 lines of output]
      /tmp/pip-build-env-nyk6ackf/overlay/lib/python3.12/site-packages/setuptools/dist.py:760: SetuptoolsDeprecationWarning: License classifiers are deprecated.
      !!
      
              ********************************************************************************
              Please consider removing the following classifiers in favor of a SPDX license expression:
      
              License :: OSI Approved :: MIT License
      
              See https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#license for details.
              ********************************************************************************
      
      !!
        self._finalize_license_expression()
      running bdist_wheel
      running build
      running build_py
      creating build/lib.linux-aarch64-cpython-312
      copying onigurumacffi.py -> build/lib.linux-aarch64-cpython-312
      running build_ext
      generating cffi module 'build/temp.linux-aarch64-cpython-312/_onigurumacffi.c'
      creating build/temp.linux-aarch64-cpython-312
      building '_onigurumacffi' extension
      creating build/temp.linux-aarch64-cpython-312/build/temp.linux-aarch64-cpython-312
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fexceptions -fexceptions -fexceptions -fPIC -I/usr/include/python3.12 -c build/temp.linux-aarch64-cpython-312/_onigurumacffi.c -o build/temp.linux-aarch64-cpython-312/build/temp.linux-aarch64-cpython-312/_onigurumacffi.o
      build/temp.linux-aarch64-cpython-312/_onigurumacffi.c:50:14: fatal error: pyconfig.h: No such file or directory
         50 | #    include <pyconfig.h>
            |              ^~~~~~~~~~~~
      compilation terminated.
      error: command '/usr/bin/gcc' failed with exit code 1
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for onigurumacffi
Failed to build onigurumacffi
ERROR: Could not build wheels for onigurumacffi, which is required to install pyproject.toml-based projects
...
```


You need to do the following ->
The error log also references a missing oniguruma.h file, indicating that the Oniguruma regular expressions library is not installed.


### Install Oniguruma Development Package:
On Fedora, you can install the Oniguruma development package using:
```
sudo dnf install oniguruma-devel
```
This will provide the necessary headers for the onigurumacffi package to compile successfully.

### Ensure all necessary development tools and libraries are installed:
```
sudo dnf groupinstall 'Development Tools'
sudo dnf install python3-devel oniguruma-devel
```

### Attempt to install ansible-dev-tools using pip: ￼
```
pip3 install --user ansible-dev-tools
```

### Verify the installation:
```
ansible-navigator --version
```