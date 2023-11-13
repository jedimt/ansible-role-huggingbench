Ansible Role: Huggingbench
==========================

Install the HuggingBench MLOps tool for benchmarking HuggingFace models

Requirements
------------

Ubuntu 22.04 and Python 3.10

Role Variables
--------------

    # huggingbench.yml variables
      # Path to receive the cloned huggingbench storage repo
      huggingbench_repo_dest_folder: '{{ ansible_env.HOME }}/github/huggingbench'

      # There are no versions/releases in the repo. This is the latest commit as of 11/8/2023
      huggingbench_github_version: "ffd8884"

      # Python version for venv used for mlperf packages and modules
      venv_python_version: '3.10'

      # Version of the NVIDIA Triton inference server to pull
      huggingbench_triton_version: "23.04-py3"

      # Controls if the NVIDIA Triton docker image is pulled
      huggingbench_pull_triton: true

      # Force git pull of huggingbench repo when there are local changes
      huggingbench_pull_repo_force: false

    # precheck.yml variables
      # Minimum tested version of python
      precheck_python_min_version: '3.10'

      # Minimum tested version of Ansible (7.x)
      precheck_ansible_min_version: '2.14.1'

      # Minimum Ubuntu version
      precheck_ubuntu_min_version: '22.04'

Example Playbook

    # ==========================================================================
    # HuggingFace installation
    # ==========================================================================
    - name: Install and configure MLPerf Storage Benchmark
      hosts: servers
      tags: play_mlperf_install
      # become: true
      gather_facts: true

      vars_files:
        # Ansible vault with all required passwords
        - "../../credentials.yml"

      roles:
        - { role: jedimt.mlperf,
            skip_validation: true
        }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
