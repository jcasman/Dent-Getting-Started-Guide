# Code contributions

We can separate two different code contribution workflows:
1. Code that is being upstreamed to the Linux Kernel
2. Code that is intended to be included in the dentOS repository

## Code that is being upstreamed to the Linux Kernel

Code that is sent to the Kernel mailing lists needs to adhere to the Linux Kernel coding and patch submission guidelines. In order to unify the coding style, Linux kernel has several preferences when it comes to the coding guidelines. Namely, the [Linux kernel coding style](https://www.kernel.org/doc/html/latest/process/coding-style.html) document mentions some useful guidelines, such as how to use tabs and spaces, writing comments, functions, etc.


In order to enhance the code submission process, Linux Kernel introduced a requirement for the [Developer Certificate of Origin](https://developercertificate.org/) (DCO). Kernel community requires a sign-off message appended to the each commit in the patch in the following format:
```
This is a commit message

Signed-off-by: Random J Developer <random@developer.example.org>
```
Note that adding sign-offs shouldn't be done manually. Git has a `-s` command-line option that will automatically add a sign-off to your commit. This will by default use the configuration found in `~/.git./config` directory. If you have authored a commit that is missing a sign-off, it can be amended to the commit with
```
git commit --amend -s
```
Commit subject should summarize changes that are part of the commit and contain no more than 50 characters. Commit body can be used to explain the changes in more detail. More information about submitting patches to the Kernel mailing list can be found [here](https://www.kernel.org/doc/html/latest/process/submitting-patches.html). And lastly, there is a [patch submission checklist](https://www.kernel.org/doc/html/latest/process/submit-checklist.html) that developers can use prior to sending the patch.


## Code that is intended to be included in the dentOS repository

Example workflow for creating a pull request to the dentOS repository:
1. Forking the dentOS repository (if there is no already existing fork that is ready to be used)
2. Creating a local copy of the repository
3. Making changes and committing them
4. Pushing changes into a separate branch of the forked repository
5. Opening a pull request on GitHub

Some useful tips when opening pull requests on GitHub:
- Make sure that pull requests are opened to the most recent git main branch, i.e. that all changes are done on top of the latest main branch
- Make sure to test all changes before opening a pull request
- If you need to update code in the existing branch, it can be done using `git commit --amend` and later force-pushing to the same branch using `git push --force`.

Additional guidelines for contributors:
- Each code submission should include an issue identifier number to reference what is being addressed by this change
- Each code submission that includes new code branches must include automated test cases to exercise the new code branches added
- Commits should be signed and DCO approved. More information on how to setup your GPG keys: https://docs.releng.linuxfoundation.org/en/latest/gpg.html
- Commits should be rebased into the latest branch's HEAD
- Additionally, we recommend the following Best Practices: https://docs.releng.linuxfoundation.org/en/latest/best-practices.html

Guidelines for Commiters/PTL:
- When performing code reviews, committers should check the following items:
    - Make sure CI versification was successful
    - Verify that the submission contains appropriate test cases
    - Verify that the commit message is explicit and is appropriate for the code being changed/added/removed
- After code is merged, the committer should make sure any post CI processing was successful
- Pull Requests require approval from the committers team for the respective repo
- New committers can be selected by performing a TSC vote

# Intellectual Property Policy (From [Dent Technical Charter](https://dent.dev/wp-content/uploads/sites/93/2020/12/DENT-Project-Technical-Charter-12-08-2020.pdf)) 

> a. Collaborators acknowledge that the copyright in all new contributions will be
> retained by the copyright holder as independent works of authorship and that no
> contributor or copyright holder will be required to assign copyrights to the
> Project.

> b. Except as described in Section 7.c., all contributions to the Project are subject to
> the following:
>
> >  i. All new inbound code contributions to the Project must be made using the following licenses (as applicable, the “Project License”):
> >    
> >    1. For code that runs in the kernel, GNU General Public License,
> >       Version 2.0, available at https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html; and
> >    2. For all other code, Eclipse Public License, Version 1.0, available at https://www.eclipse.org/org/documents/epl-v10.html.
> >
> > ii. All new inbound code contributions must also be accompanied by a Developer Certificate of Origin (http://developercertificate.org) sign-off in the source code system that is submitted through a TSC-approved contribution process which will bind the authorized contributor and, if not self-employed, their employer to the applicable license;
> 
> > iii. All outbound code will be made available under the Project License.
> 
> >  iv. Documentation will be received and made available by the Project under the Creative Commons Attribution 4.0 International License, available at ttp://creativecommons.org/licenses/by/4.0/.
> 
>>   v. The Project may seek to integrate and contribute back to other open source projects (“Upstream Projects”). In such cases, the Project will conform to all license requirements of the Upstream Projects, including dependencies, leveraged by the Project. Upstream Project code contributions not stored within the Project’s main code repository will comply with the contribution process and license terms for the applicable Upstream Project.

> c. The TSC may approve the use of an alternative license or licenses for inbound or outbound contributions on an exception basis. To request an exception, please describe the contribution, the alternative open source license(s), and the justification for using an alternative open source license for the Project. License exceptions must be approved by a two-thirds vote of the entire TSC.

> d. Contributed files should contain license information, such as SPDX short form identifiers, indicating the open source license or licenses pertaining to the file.
