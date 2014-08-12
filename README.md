## Feature Development

### Installation - Cloning

git clone https://github.com/balancedthought/madden_ocp.git

### Basic Steps

<ol>
	<li>Git Fetch to update your staging repository</li>
        <li>Pull to update your local Release Branch</li>
	<li>Check out a feature branch</li>
	<li>Do work in your feature branch, committing early and often</li>
	<li>Rebase frequently to incorporate upstream changes</li>
	<li>Interactive rebase (squash) your commits</li>
	<li>Notify QA of your completed feature</li>
	<li>Once your feature has been approved by QA</li>
	<ol>
		<li>Rebase once again from the Release Branch</li>
		<li>Merge your changes into the Release Branch</li>
		<li>Push your changes upstream</li>
                <li>Delete your remote branch</li>
	</ol>
</ol>

#### Branch naming conventions

> "#{developer_initials}_#{trello_card_number_only_numbers}_#{trello_card_brief_description.gsub(/\s/,'_')}".downcase

e.g.: 
developer name: Viorel Leganaru
trello card number: 48
card's desc: Add a new Store Interface

==> vl_48_fix_add_a_new_store_interface

Should match: @/^[a-z]{2,3}_\d{1,5}(_[0-9a-z]+)+$/@

;-)

### Steps in Depth        

#### Background Info

The Release Branch is *rb_2012_04_03*
_Your Name is Dinesh Panchal_
_Your initials are *dp*_
_Your trello card number is *35*_

#### Before you begin you must use this command

> git config branch.autosetuprebase always
git config branch.master.rebase true

The code above will make your git pull command default to always add - -rebase


<ol>
<li> 
#### +Pull to update your local Release Branch+


@git checkout --track origin/rb_2012_04_03@	
@git pull origin rb_2012_04_03@

<p>this will create a local branch named rb_2012_04_03</p>
</li>
<li>
#### +Check out a feature branch+

@git checkout -b dp_35_country_validations@

<p>_*your initials + trello card number + small description (all lowercase)*_</p>
</li>
<li>
#### +Do work in your feature branch, committing early and often+


@#do your work@
@git add foo.rb@
@git commit -m "WIP: hacking on this and that"@
@#do more work@
@git add  bar.rb@
@git commit -m "COMPLETED: tests and all"@
</li>
<li>
#### +Rebase frequently to incorporate upstream changes+


	@git fetch@
	@git rebase origin/rb_2012_04_03@	

</li>
<li>
#### +Interactive rebase (squash) your commits+

	@git rebase -i rb_2012_04_03@

<h5> 
*Git will display an editor window with a list of the commits to be modified, something like:*

	@pick 3dcd585 Adding Comment blah@
	@pick 9f5c362 Adding Comment something important@ 
	@pick dcd4813 Adding Comment video on product page@ 
	@pick 977a754 Adding Comment update cart@ 
	@pick 9ea48e3 Adding Comment bubbles make me smile@ 

*Now we tell git what we to do. Change these lines to:*

	@pick 3dcd585 Adding Comment blah@
	@squash 9f5c362 Adding Comment something important@ 
	@squash dcd4813 Adding Comment video on product page@ 
	@squash 977a754 Adding Comment update cart@ 
	@squash 9ea48e3 Adding Comment bubbles make me smile@ 

</h5>
</li>
<li>
#### +Notify QA of your completed feature+

h5. You can do this by following the steps below: 
</li>
<ol>
       <li>move your card from the 'In Progress' list to the 'Test' list</li>
       <li>add the qa person to the card</li>
       <li>add a comment to the card's activity stream which will notify the appropriate qa person that was added in step 2</li>
</ol>
<li>
#### +Once your feature has been approved by QA+		
</li>
<ol>
<li>
#### +Rebase once again from the Release Branch+

	@git fetch@
	@git rebase origin/rb_2012_04_03@	

</li>
<li>
#### +Merge your changes into the Release Branch+

	@git checkout rb_2012_04_03@
	@git merge dp_35_country_validations@	

</li>
<li>
#### +Push your changes upstream+


	@git push origin rb_2012_04_03@

</li>
<li>
#### +After your feature has been merged into master, delete your remote branch+

	@git push origin :dp_35_country_validations@

</li>
</ol>	
</ol>


## Feature Development with multiple developers

#### push your local branch to github

@git push origin branch_name@
@git branch --set-upstream branch_name origin/branch_name@

##### Then, others can check out your changes with a git fetch and a git checkout.

@git fetch@
@git checkout --track origin/branch_name@

##### Use the same exact steps as above treating the shared branch as the release branch. You cannot rebase commits that have been pushed remotely, unless all the people who have downloaded the branch agree to delete the branch and re-download.

## BugFixes for production not associated to a release 

#### The only difference from the steps above is

<ul>
	<li>Use the master branch instead of the release branch</li>
	<li>ONLY have ONE commit(squashed)</li>
	<li>do NOT have a partial fix</li>
</ul>

## Further Reading

"A Git Workflow for Agile Teams":http://reinh.com/blog/2009/03/02/a-git-workflow-for-agile-teams.html
"A successful Git branching model":http://nvie.com/posts/a-successful-git-branching-model/
"The Case for Git Rebase":http://darwinweb.net/articles/the-case-for-git-rebase
"The ProGit Book":http://progit.org/book/



