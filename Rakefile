GH_REPOSITORY = 'git@github.com:kay8/kaffee-kantate.git'


desc 'setup for cleaning up _deploy directory'
task :setup do
  sh 'rm -rf _deploy'
  sh "git clone #{GH_REPOSITORY} _deploy"
  cd '_deploy' do
    sh 'git checkout gh-pages'
  end
end

desc 'deploy to github pages'
task :deploy do
  sh 'bundle exec jekyll'
  sh 'rm -rf _deploy/*'
  sh 'cp -R _site/* _deploy'
  cd '_deploy' do
    sh 'git add -A'
    sh 'git commit -v'
    sh 'git push origin gh-pages'
  end
end