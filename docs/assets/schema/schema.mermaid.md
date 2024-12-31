```mermaid
erDiagram
    chat_conversation {
        id integer_NOT_NULL
        name text_NOT_NULL
        model ai_model_enum_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
    }
    chat_conversation_file {
        id integer_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
        chat_conversation_id integer_NOT_NULL
        chat_conversation_message_id integer_NOT_NULL
        neptun_user_file_id integer_NOT_NULL
    }
    chat_conversation_message {
        id integer_NOT_NULL
        message text_NOT_NULL
        actor chat_conversation_message_actor_enum
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
        chat_conversation_id integer_NOT_NULL
    }
    chat_conversation_share {
        id integer_NOT_NULL
        is_shared boolean_NOT_NULL
        share_id uuid_NOT_NULL
        is_protected boolean_NOT_NULL
        hashed_password text
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        chat_conversation_id integer_NOT_NULL
    }
    chat_conversation_share_whitelist_entry {
        id integer_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        whitelisted_neptun_user_id integer_NOT_NULL
        chat_conversation_share_id integer_NOT_NULL
    }
    github_app_installation {
        id integer_NOT_NULL
        github_account_type text_NOT_NULL
        github_account_avatar_url text_NOT_NULL
        github_account_id integer_NOT_NULL
        github_account_name text
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
    }
    github_app_installation_repository {
        id integer_NOT_NULL
        github_repository_id integer_NOT_NULL
        github_repository_name text_NOT_NULL
        github_repository_description text
        github_repository_size integer
        github_repository_language text
        github_repository_license text
        github_repository_url text_NOT_NULL
        github_repository_website_url text
        github_repository_default_branch text
        github_repository_is_private boolean_NOT_NULL
        github_repository_is_fork boolean
        github_repository_is_template boolean
        github_repository_is_archived boolean_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        github_app_installation_id integer_NOT_NULL
    }
    neptun_user {
        id integer_NOT_NULL
        primary_email text_NOT_NULL
        hashed_password text
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
    }
    neptun_user_oauth_account {
        id integer_NOT_NULL
        provider oauth_provider_enum_NOT_NULL
        oauth_user_id text_NOT_NULL
        oauth_email text_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
    }
    neptun_user_file {
        id integer_NOT_NULL
        title text
        text text_NOT_NULL
        language text
        file_extension text
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
    }
    neptun_user_template {
        id integer_NOT_NULL
        description text
        file_name text_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
        template_collection_id integer
        user_file_id integer
    }
    neptun_user_template_collection {
        id integer_NOT_NULL
        name text_NOT_NULL
        description text
        is_shared boolean_NOT_NULL
        share_id uuid_NOT_NULL
        created_at timestamp_without_time_zone
        updated_at timestamp_without_time_zone
        neptun_user_id integer_NOT_NULL
    }

    chat_conversation_file }o--|| chat_conversation : "references"
    chat_conversation_file }o--|| chat_conversation_message : "references"
    chat_conversation_file }o--|| neptun_user_file : "references"
    chat_conversation_file }o--|| neptun_user : "references"
    chat_conversation_message }o--|| chat_conversation : "references"
    chat_conversation_message }o--|| neptun_user : "references"
    chat_conversation }o--|| neptun_user : "references"
    chat_conversation_share }o--|| chat_conversation : "references"
    chat_conversation_share_whitelist_entry }o--|| chat_conversation_share : "references"
    chat_conversation_share_whitelist_entry }o--|| neptun_user : "references"
    github_app_installation }o--|| neptun_user : "references"
    github_app_installation_repository }o--|| github_app_installation : "references"
    neptun_user_file }o--|| neptun_user : "references"
    neptun_user_oauth_account }o--|| neptun_user : "references"
    neptun_user_template_collection }o--|| neptun_user : "references"
    neptun_user_template }o--|| neptun_user : "references"
    neptun_user_template }o--|| neptun_user_template_collection : "references"
    neptun_user_template }o--|| neptun_user_file : "references"

```