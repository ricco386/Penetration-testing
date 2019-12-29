Penetration testing - Personal study notes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This are my personal notes taken during the path into security.

In this notes there are topics I have found interesting and wanted to learn. What has worked for me might not work for you, but if you think I made a mistake somewhere feel free to submit PR. Any knowledge learned from this notes should be used wisely and legally, but most importantly you are using it at your own responsibility.

All of my study notes are released under `MIT license <https://github.com/ricco386/Penetration-testing/blob/master/LICENSE>`_, there is no guarantee anything here will work (for you), and I take **NO responsibility** for any illegal actions made after reading my notes.

Feel free to use them during your study and if you find it useful you can star this repository. If you find a mistake or you think I have  missed something important I am more than happy to accept RP on this repo.

Notes are written in `Sphinx <https://www.sphinx-doc.org/en/master/>`_ documentation format. You can visit build notes at url: https://ricco386.github.io/Penetration-testing/

How to build the notes
======================

Create Python virtual environments and activate them::

	python3 -m venv envs3
	source envs3/bin/activate

Install the requiremetns::

	pip install -r requirements.txt

Build the Sphinx docs::

        make html

Run Python build-in webserver and open the build documentation in browser::

	cd docs/html
	python -m http.server 8000
	firefox http://localhost:8000/

Other notes
===========

Study notes from `RITx: CYBER501x Cybersecurity Fundamentals <https://www.edx.org/course/cybersecurity-fundamentals>`_ at `edx.org <https://www.edx.org/>`_ are available here:

* `CYBER501x Cybersecurity Fundamentals notes <https://github.com/ricco386/CYBER501x-Cybersecurity-Fundamentals>`_
* `CYBER502x Computer Forensics notes <https://github.com/ricco386/CYBER502x-Computer-Forensics>`_


Richard von Kellner