# Podfile

use_frameworks!

target "AppTacToe" do
  inherit! :search_paths

  abstract_target 'Tests' do
    target "AppTacToeTests"

    pod 'Quick', '~> 2.2'
    pod 'Nimble', '~> 8.1'
  end
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    if target.name == "Nimble"
      target.build_configurations.each do |config|
          xcconfig_path = config.base_configuration_reference.real_path
          xcconfig = File.read(xcconfig_path)
          new_xcconfig = xcconfig.sub('lswiftXCTest', 'lXCTestSwiftSupport')
          File.open(xcconfig_path, "w") { |file| file << new_xcconfig }
      end
    else
      target.build_configurations.each do |config|
        config.build_settings.delete 'IPHONEOS_DEPLOYMENT_TARGET'
      end
    end
  end
end
