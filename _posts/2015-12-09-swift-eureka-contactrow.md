---
id: 384
title: Eureka ContactRow in Swift
date: 2015-12-09T01:58:51+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=384
permalink: /swift-eureka-contactrow/
thumb_image: /wp-content/uploads/2015/12/code-1084923-256x256.png
tags:
  - Swift
---
A custom row for the [elegant iOS form builder in Swift 2 called Eureka](https://github.com/xmartlabs/Eureka):

<a href="http://blog.marco.betschart.name/wp-content/uploads/2015/12/ContactRow.gif" rel="attachment wp-att-398" class="broken_link"><img class="aligncenter wp-image-398 size-full" src="http://blog.marco.betschart.name/wp-content/uploads/2015/12/ContactRow.gif" alt="ContactRow" width="375" /></a>

Select an existing contact from the iOS AddressBook using the new iOS 9 CNContact API &#8211; [request for integration pending](https://github.com/xmartlabs/Eureka/issues/127).

<div class="snippetcpt-wrap" id="snippet-496" data-id="496" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=496&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=496" data-fullscreen="http://dev.marco-betschart.local/code-snippets/eureka-contactrow/?full-screen=1">
  <pre class="prettyprint linenums lang-swift" title="Eureka ContactRow">import Foundation
import Contacts
import ContactsUI
import Eureka


public class _ContactRow: Row&lt;String,ContactCell&gt; {
    required public init(tag: String?){
        super.init(tag: tag)
    }
}


public final class ContactRow: _ContactRow, RowType{

    required public init(tag: String?) {
        super.init(tag: tag)
        self.displayValueFor = nil
    }
}

public class ContactCellOf&lt;T: Equatable&gt;: Cell&lt;T&gt;, CellType, CNContactPickerDelegate {
    required public init(style: UITableViewCellStyle, reuseIdentifier: String?) {
        super.init(style: style, reuseIdentifier: reuseIdentifier)
    }


    public override func setup(){
        super.setup()
        self.bindContact()
    }


    public override func update() {
        super.update()
        self.bindContact()
    }


    private func bindContact(){
        switch CNContactStore.authorizationStatusForEntityType(.Contacts){
        case .Authorized: //Update our UI if the user has granted access to their Contacts
            selectionStyle = row.isDisabled ? .None : .Default

            if let id = self.row.value as? String, let contact = contactFromIdentifier(id){
                detailTextLabel?.text = CNContactFormatter.stringFromContact(contact, style: .FullName)
            }

        case .NotDetermined: //Prompt the user for access to Contacts if there is no definitive answer
            CNContactStore().requestAccessForEntityType(.Contacts) { granted, error in
                dispatch_async(dispatch_get_main_queue()){
                    self.row.disabled = Condition.init(booleanLiteral: !granted)
                    self.selectionStyle = self.row.isDisabled ? .None : .Default

                    if granted, let id = self.row.value as? String, let contact = self.contactFromIdentifier(id){
                        self.detailTextLabel?.text = CNContactFormatter.stringFromContact(contact, style: .FullName)
                    }
                }
            }

        case .Denied, .Restricted:
            self.row.disabled = true
            selectionStyle = row.isDisabled ? .None : .Default
        }
    }


    private func contactFromIdentifier(identifier: String) -&gt; CNContact?{
        do{
            return try CNContactStore().unifiedContactWithIdentifier(identifier, keysToFetch: [CNContactFormatter.descriptorForRequiredKeysForStyle(.FullName)])

        } catch let error as NSError{
            NSLog(error.localizedDescription)
            return nil
        }
    }


    public override func didSelect() {
        super.didSelect()

        let controller = CNContactPickerViewController()
        controller.delegate = self

        self.formViewController()?.presentViewController(controller, animated: true, completion: nil)
    }


    public func contactPicker(picker: CNContactPickerViewController, didSelectContactProperty contactProperty: CNContactProperty){
        if contactProperty.contact.isKeyAvailable(CNContactIdentifierKey), let id = contactProperty.contact.valueForKey(CNContactIdentifierKey) as? T{
            self.row.value = id

        } else {
            self.row.value = nil
        }
    }
}
public typealias ContactCell = ContactCellOf&lt;String&gt;</pre>
</div>