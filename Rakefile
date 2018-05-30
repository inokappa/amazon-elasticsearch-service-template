namespace :es do
  targets = []
  Dir.glob('./parameters/*').each do |dir|
    target = File.basename(dir)
    targets << target.split('.')[0]
  end

  namespace :check do
    desc "全環境の cloudformation stack テンプレートの validate をチェックする"
    task :all     => targets

    targets.each do |target|
      desc "#{target} の cloudformation stack テンプレートの validate をチェックする"
      task target.to_sym do
        sh "./deploy.sh ${AWS_PROFILE} ${STACK_NAME_PREFIX} #{target} validate"
      end
    end
  end

  namespace :create do
    targets.each do |target|
      desc "#{target} の cloudformation stack を作成する"
      task target.to_sym do
        sh "./deploy.sh ${AWS_PROFILE} ${STACK_NAME_PREFIX} #{target} create"
      end
    end
  end

  namespace :update do
    targets.each do |target|
      desc "#{target} の cloudformation stack を更新する"
      task target.to_sym do
        sh "./deploy.sh ${AWS_PROFILE} ${STACK_NAME_PREFIX} #{target} update"
      end
    end
  end

  namespace :delete do
    targets.each do |target|
      desc "#{target} の cloudformation stack を削除する"
      task target.to_sym do
        sh "./deploy.sh ${AWS_PROFILE} ${STACK_NAME_PREFIX} #{target} delete"
      end
    end
  end
end
