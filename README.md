# Why?

https://github.com/hashicorp/terraform/issues/516

Secrets in git are a no-no. 

# How?

Some bash, sed, black magic. 

# Usage

```
$ cat aws_access_key
<redacted>
$ cat aws_secret_key
<redacted>
$ cat terraform.tfstate | grep ses
"ses_smtp_password": "<redacted>",
./terraformectomy <redacted> <redacted> <redacted>
$ cat terraform.tfstate | grep ses
                            "ses_smtp_password": "CENSORED_BY_TERRAFORMECTOMY",
```

# Problems

Terraform will often try to check that the AWS access keys are valid, and wants to reprovision them. Still better than not commiting the state file at all. This is a (hopefully) temporary thing until Hashicorp gets around to fixing terraform. I have doubts since the issue is from 2014 and still no progress. Hopefully `terraformectomy` is a quick bandaid. 
