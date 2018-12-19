
# Sample Dev Ops Tool

  

## Overview

  

Here is some text describing a dev ops tool that I have wrote about here.

**Here's some more information regarding this tool. It's really great. Etc, etc.**

## Sample code 

		data  "template_cloudinit_config"  "guacdeploy_config"  {

			gzip  =  false

			base64_encode  =  false

		  

		part {

			filename  =  "guacconfig.cfg"

			content_type  =  "text/cloud-config"

			content  =  "${data.template_file.guacdeploy.rendered}"

		}

	}